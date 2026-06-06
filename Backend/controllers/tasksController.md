# src/controllers/tasksController.js

Controlador para la gestión de tareas del usuario. Cubre creación, listado, actualización de estado, eliminación y resumen diario con recomendación motivacional.

## Funciones exportadas

### `listByUser(req, res)`

Lista todas las tareas de un usuario ordenadas por fecha de creación descendente.

**Parámetros de ruta:** `userId`

- Llama a `tasksService.listTasksByUser(userId)`.
- Devuelve `200` con el array de tareas.

**Ruta asociada:** `GET /tasks/:userId/list`

---

### `create(req, res)`

Crea una nueva tarea para el usuario. Acepta múltiples variantes de nombres de campo para facilitar la integración con distintos clientes.

**Parámetros de ruta:** `userId`  
**Cuerpo (cualquier variante):**

| Campo canónico         | Variantes aceptadas                                         |
|------------------------|-------------------------------------------------------------|
| `name`                 | `name`, `title`, `titulo`, `nombre`                        |
| `description`          | `description`, `descripcion`                               |
| `due_date`             | `due_date`, `dueDate`, `fechaFin`, `fecha_fin`             |
| `estimated_time_hours` | `estimated_time_hours`, `estimatedTime`, `tiempoEstimado`, `tiempo_estimado` |
| `attachment_link`      | `attachment_link`, `attachmentLink`, `linkAdjunto`, `link_adjunto` |
| `priority`             | `priority`, `prioridad`, `prioridadTarea`                  |

- Requiere `userId` y un nombre de tarea; devuelve `400` si faltan.
- Llama a `tasksService.createTask(...)`.
- Devuelve `201` con la tarea creada.

**Ruta asociada:** `POST /tasks/:userId/create`

---

### `updateStatus(req, res)`

Actualiza el estado de una tarea existente.

**Parámetros de ruta:** `taskId`  
**Cuerpo:** `{ status: "pending" | "in_progress" | "done" }` (también acepta `estado`, `estadoTarea`)

- Valida que `status` sea uno de los tres valores permitidos; devuelve `400` si es inválido.
- Devuelve `404` si la tarea no existe.
- Llama a `tasksService.updateTaskStatus({ taskId, status })`.
- Devuelve `200` con la tarea actualizada.

**Ruta asociada:** `PATCH /tasks/:taskId/status`

---

### `remove(req, res)`

Elimina una tarea por su ID.

**Parámetros de ruta:** `taskId`

- Devuelve `404` si la tarea no existe.
- Llama a `tasksService.deleteTask(taskId)`.
- Devuelve `200` con `{ message: "Tarea eliminada", task }`.

**Ruta asociada:** `DELETE /tasks/:taskId`

---

### `getDailySummary(req, res)`

Resumen de tareas para una fecha específica junto con una recomendación generada localmente.

**Parámetros de ruta:** `userId`  
**Query params:** `date` (YYYY-MM-DD, opcional; por defecto: hoy)

- Valida formato de fecha si se provee; devuelve `400` si es inválido.
- Llama a `tasksService.getDailySummaryByUser({ userId, date })`.
- Genera una recomendación motivacional con `buildRecommendation(...)` según la carga de trabajo:

  | Condición                                      | Mensaje                                                          |
  |------------------------------------------------|------------------------------------------------------------------|
  | Sin tareas programadas                         | "No tienes tareas programadas hoy. Aprovecha para planificar o descansar." |
  | Todas las tareas completadas                   | "Buen trabajo, ya completaste todas tus tareas de hoy."          |
  | ≥5 pendientes o ≥70% del total                 | "Tienes una carga alta hoy. Toma pausas activas y prioriza tus tareas." |
  | Resto                                          | "Vas bien. Mantente enfocado y avanza paso a paso."              |

- Devuelve `200` con `{ date, tasksScheduled, tasksDone, tasksPending, recommendation }`.

**Ruta asociada:** `GET /summary/:userId`

## Códigos de respuesta comunes

| Código | Descripción                           |
|--------|---------------------------------------|
| `200`  | Operación exitosa.                    |
| `201`  | Tarea creada correctamente.           |
| `400`  | Parámetro faltante o inválido.        |
| `404`  | Tarea no encontrada.                  |
| `500`  | Error interno del servidor.           |

## Dependencias

- `../services/tasksService`
