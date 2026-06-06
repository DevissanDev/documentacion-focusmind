# Servicio: API Client

**Archivo**: [src/services/apiClient.js](../../src/services/apiClient.js)

Cliente HTTP centralizado que envuelve `fetch` con autenticación JWT automática via AWS Cognito. Todas las llamadas a la API del backend pasan por aquí.

## Función principal: `apiFetch`

```js
import { apiFetch } from '../services/apiClient'

const response = await apiFetch('/tasks/user123/list')
const data = await response.json()
```

### Firma

```ts
apiFetch(path: string, options?: RequestInit): Promise<Response>
```

| Parámetro | Tipo | Descripción |
|-----------|------|-------------|
| `path` | `string` | Ruta relativa al `VITE_API_URL` (ej: `/tasks/user1/list`) |
| `options` | `RequestInit?` | Opciones estándar de `fetch` (method, headers, body, etc.) |

Retorna la misma `Response` que retornaría `fetch` nativo.

## Comportamiento de autenticación

1. Obtiene el `accessToken` de la sesión activa de AWS Cognito via `fetchAuthSession()`
2. Inyecta el header `Authorization: Bearer <token>` en cada request
3. Si el servidor responde con `401 Unauthorized`:
   - Fuerza el refresh del token con `fetchAuthSession({ forceRefresh: true })`
   - Si obtiene un nuevo token diferente, reintenta el request original una vez
   - Si el token no cambió (ya era el más reciente), retorna la respuesta 401 original

## Configuración

La URL base se toma de la variable de entorno `VITE_API_URL`:

```env
VITE_API_URL=https://api.focusmind.com
```

Si la variable no está definida, `API_URL` será `undefined` y los requests fallarán.

## Uso en los servicios de features

Todos los archivos `*Api.js` de cada feature importan `apiFetch` directamente:

```js
// src/features/task/services/taskApi.js
import { apiFetch } from '../../../services/apiClient'

export async function fetchTasks(userId) {
  const response = await apiFetch(`/tasks/${encodeURIComponent(userId)}/list`)
  if (!response.ok) throw new Error('No se pudieron cargar las tareas.')
  return response.json()
}
```

## Consideraciones de seguridad

- Los `userId` y otros parámetros de ruta se pasan por `encodeURIComponent()` en cada servicio para prevenir path injection
- El token de acceso nunca se almacena en `localStorage` — siempre se obtiene desde la sesión de Amplify en memoria
- El refresh automático al 401 evita que el usuario vea errores de sesión expirada en flujos normales
