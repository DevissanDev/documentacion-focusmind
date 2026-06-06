# src/routes/tasksRoutes.js

Router para la gestión de tareas del usuario. Todas las rutas requieren autenticación Cognito.

## Rutas

| Método    | Ruta                        | Auth    | Controlador                        | Descripción                          |
|-----------|-----------------------------|---------|------------------------------------|--------------------------------------|
| `GET`     | `/summary/:userId`          | Cognito | `tasksController.getDailySummary`  | Resumen diario con recomendación.    |
| `GET`     | `/tasks/:userId/list`       | Cognito | `tasksController.listByUser`       | Lista todas las tareas del usuario.  |
| `POST`    | `/tasks/:userId/create`     | Cognito | `tasksController.create`           | Crea una nueva tarea.                |
| `PATCH`   | `/tasks/:taskId/status`     | Cognito | `tasksController.updateStatus`     | Actualiza el estado de una tarea.    |
| `DELETE`  | `/tasks/:taskId`            | Cognito | `tasksController.remove`           | Elimina una tarea.                   |

Este router se monta bajo el prefijo `/` en `app.js`.

## Dependencias

- `express`
- `../controllers/tasksController`
- `../middlewares/cognitoAuth`
