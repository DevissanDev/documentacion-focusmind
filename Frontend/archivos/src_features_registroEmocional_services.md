# src/features/registroEmocional/services/registroEmocionalApi.js

Proposito
- Encapsular llamadas al endpoint de registros emocionales.

Responsabilidades
- Llamar a `/emotionalrecords/:userId/list`.
- Validar `response.ok` antes de devolver JSON.

Flujo basico
1) Construir URL con `userId`.
2) Ejecutar request via `apiFetch`.
3) Validar estado HTTP y devolver JSON.

Entradas/Salidas
- Entradas: `userId`.
- Salidas: lista de registros emocionales.

Dependencias
- ../../services/apiClient

Notas
- Requiere `VITE_API_URL` configurada.

Ejemplo
```js
// registroEmocionalApi.list(userId)
```
