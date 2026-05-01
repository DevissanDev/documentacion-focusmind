# src/controllers/tasksController.js

Proposito
- Exponer endpoints para tareas.
- Delegar consultas a la capa de servicio.

Responsabilidades
- Leer `userId` desde params.
- Retornar lista de tareas o error.

Flujo basico
1) Extraer `userId`.
2) Llamar `listTasksByUser`.
3) Responder con JSON o 500.

Entradas/Salidas
- Entradas: `req.params.userId`.
- Salidas: JSON con tareas o error.

Dependencias
- ../services/tasksService

Notas
- Responde 500 ante fallas de DB o servicio.

Ejemplo
```js
// GET /tasks/123/list
```
