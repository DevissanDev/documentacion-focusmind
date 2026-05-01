# src/services/apiClient.js

Proposito
- Centralizar llamadas HTTP al backend.
- Adjuntar token de Cognito en el header.

Responsabilidades
- Obtener `access_token` con `fetchAuthSession`.
- Agregar `Authorization: Bearer` a cada request.
- Reintentar en 401 con `forceRefresh`.

Flujo basico
1) Resolver base URL desde `VITE_API_URL`.
2) Obtener token de Cognito.
3) Ejecutar `fetch` con headers.
4) Reintentar si hay 401 y refrescar sesion.

Entradas/Salidas
- Entradas: path, options de request y session actual.
- Salidas: respuesta JSON o error.

Dependencias
- aws-amplify
- fetch (browser)

Notas
- Requiere `VITE_API_URL` en el entorno.
- Si no existe, se generan URLs `undefined/...`.

Ejemplo
```js
// apiFetch("/tasks/123/list")
```
