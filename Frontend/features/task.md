# Feature: Tareas

Gestión completa de tareas del usuario (CRUD). Permite crear, listar, actualizar el estado y eliminar tareas asociadas a la cuenta del usuario autenticado.

## Archivos relevantes

```
src/features/task/
├── components/
│   ├── TaskList.jsx           # Lista principal de tareas con filtros
│   ├── TaskDetailModal.jsx    # Modal para ver y editar detalle de tarea
│   ├── CreateTaskPanel.jsx    # Panel lateral para crear nueva tarea
│   ├── SidePanel.jsx          # Panel lateral genérico (wrapper)
│   └── Modal.jsx              # Componente modal reutilizable
├── hooks/
│   └── useTasks.js            # Estado y operaciones de tareas
└── services/
    └── taskApi.js             # Llamadas a la API de tareas
```

```
src/pages/TaskPage.jsx         # Página que ensambla la feature
```

## API

Base path: `/tasks`

| Función | Método | Endpoint | Descripción |
|---------|--------|----------|-------------|
| `fetchTasks(userId)` | GET | `/tasks/:userId/list` | Listar todas las tareas del usuario |
| `createTask(userId, data)` | POST | `/tasks/:userId/create` | Crear una nueva tarea |
| `updateTaskStatus(taskId, status)` | PATCH | `/tasks/:taskId/status` | Actualizar estado de una tarea |
| `deleteTask(taskId)` | DELETE | `/tasks/:taskId` | Eliminar una tarea |

### Payload de creación de tarea

```json
{
  "title": "string",
  "status": "pendiente | en_progreso | completada",
  "dueDate": "YYYY-MM-DD",
  "estimatedDuration": "number (minutos)",
  "priority": "alta | media | baja"
}
```

## Hook: `useTasks`

Gestiona el estado local de tareas y expone operaciones memoizadas.

```js
const {
  tasks,          // Task[]
  loading,        // boolean
  error,          // string | null
  createTask,     // (data) => Promise<void>
  updateStatus,   // (taskId, status) => Promise<void>
  deleteTask,     // (taskId) => Promise<void>
  refetch,        // () => Promise<void>
} = useTasks()
```

Obtiene el `userId` del usuario autenticado via `getCurrentUser()` de AWS Amplify al montar.

## Componentes principales

### `TaskList`

Renderiza la lista de tareas con soporte para:
- Filtrado por estado (pendiente / en progreso / completada)
- Seleccionar tarea para ver detalle
- Botón para abrir `CreateTaskPanel`
- Estado vacío cuando no hay tareas

### `TaskDetailModal`

Modal que muestra el detalle completo de una tarea seleccionada:
- Título, estado, fecha vencimiento, prioridad, duración estimada
- Botón para cambiar el estado
- Botón para eliminar la tarea

### `CreateTaskPanel`

Panel lateral (slide-in) con formulario para crear nueva tarea:
- Campos: título, fecha vencimiento, prioridad, duración estimada
- Validación básica antes de enviar
- Cierra automáticamente al crear con éxito

## Ruta

`/tareas` — renderizada en `TaskPage` dentro del `DashboardShell`.
