# src/features/task/services/taskApi.js

Proposito
- Encapsular llamadas al endpoint de tareas.

Responsabilidades
- Llamar a `/tasks/:userId/list`.
- Validar `response.ok` antes de devolver JSON.

Flujo basico
1) Construir URL con `userId`.
2) Ejecutar request via `apiFetch`.
3) Validar estado HTTP y devolver JSON.

Entradas/Salidas
- Entradas: `userId`.
- Salidas: lista de tareas.

Dependencias
- ../../services/apiClient

Notas
- Requiere `VITE_API_URL` configurada.

Ejemplo
```js
// taskApi.list(userId)
```
