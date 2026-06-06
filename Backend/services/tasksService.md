# src/services/tasksService.js

Servicio para la gestión de tareas. Encapsula todas las operaciones CRUD sobre la tabla `tasks` y el resumen diario.

## Funciones exportadas

### `listTasksByUser(userId)`

Retorna todas las tareas de un usuario ordenadas por fecha de creación descendente.

**SQL:** `SELECT ... FROM tasks WHERE user_id = $1 ORDER BY created_at DESC`

**Retorna:** Array de tareas con todos los campos de la tabla.

---

### `createTask({ userId, name, description, dueDate, estimatedTimeHours, attachmentLink, priority })`

Inserta una nueva tarea. Los valores vacíos o `undefined` se normalizan a `null` antes de la inserción.

**SQL:** `INSERT INTO tasks (...) VALUES ($1...$7) RETURNING *`

**Retorna:** El objeto de la tarea recién creada con todos sus campos.

---

### `updateTaskStatus({ taskId, status })`

Actualiza el campo `status` de una tarea y registra la fecha/hora de modificación.

**SQL:** `UPDATE tasks SET status = $1, updated_at = NOW() WHERE id = $2 RETURNING *`

**Retorna:** La tarea actualizada, o `undefined` si no existe.

---

### `deleteTask(taskId)`

Elimina una tarea y retorna sus datos antes de borrarla.

**SQL:** `DELETE FROM tasks WHERE id = $1 RETURNING *`

**Retorna:** La tarea eliminada, o `undefined` si no existe.

---

### `getDailySummaryByUser({ userId, date })`

Cuenta las tareas del usuario agrupadas por estado para una fecha específica. Si `date` es `null`, usa `CURRENT_DATE`.

**SQL:**
```sql
SELECT
  to_char(COALESCE($2::date, CURRENT_DATE), 'YYYY-MM-DD') AS date,
  COUNT(*)::int AS tasks_scheduled,
  COUNT(*) FILTER (WHERE status = 'done')::int AS tasks_done,
  COUNT(*) FILTER (WHERE status IN ('pending', 'in_progress'))::int AS tasks_pending
FROM tasks
WHERE user_id = $1
  AND DATE(due_date) = COALESCE($2::date, CURRENT_DATE);
```

**Retorna:**
```json
{
  "date": "2025-01-15",
  "tasks_scheduled": 5,
  "tasks_done": 3,
  "tasks_pending": 2
}
```

## Función auxiliar interna

### `normalizeValue(value)`

Convierte `undefined`, `null` o strings vacías a `null`. Preserva cualquier otro valor. Se aplica a todos los campos opcionales antes de insertar en la base de datos.

## Esquema de la tabla `tasks`

| Columna                 | Tipo        | Descripción                           |
|-------------------------|-------------|---------------------------------------|
| `id`                    | UUID/serial | Identificador único.                  |
| `user_id`               | string      | Cognito sub del propietario.          |
| `name`                  | string      | Nombre o título de la tarea.          |
| `status`                | enum        | `pending`, `in_progress`, `done`.     |
| `description`           | string      | Descripción opcional.                 |
| `due_date`              | date        | Fecha de vencimiento.                 |
| `estimated_time_hours`  | numeric     | Tiempo estimado en horas.             |
| `priority`              | string      | Prioridad de la tarea.                |
| `attachment_link`       | string      | URL de adjunto opcional.              |
| `developed_time_hours`  | numeric     | Tiempo real invertido (solo lectura). |
| `created_at`            | timestamp   | Fecha de creación.                    |
| `updated_at`            | timestamp   | Última actualización.                 |

## Dependencias

- `./postgresClient` (instancia `pool`)
