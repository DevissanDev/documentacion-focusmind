# Componentes: Tareas

Componentes que conforman la página de gestión de tareas (`/tareas`). Viven en `src/features/task/components/`.

---

## `TaskList`

**Archivo**: [src/features/task/components/TaskList.jsx](../../src/features/task/components/TaskList.jsx)

Componente principal de la feature. Renderiza el listado completo de tareas con filtros de estado y acciones de fila.

```jsx
<TaskList
  tasks={tasks}
  onTaskSelect={(task) => setSelected(task)}
  onCreateClick={() => setPanelOpen(true)}
  loading={loading}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `tasks` | `Task[]` | Array de tareas a listar |
| `onTaskSelect` | `(task: Task) => void` | Callback al hacer clic en una tarea |
| `onCreateClick` | `() => void` | Callback del botón "Nueva tarea" |
| `loading` | `boolean` | Muestra skeleton mientras carga |

**Funciones de la UI**:
- Tabs o chips para filtrar por estado (`pendiente`, `en_progreso`, `completada`)
- Íconos de prioridad con colores (alta=rojo, media=amarillo, baja=verde)
- Fecha de vencimiento con indicador de vencida (color rojo si pasó)
- Estado vacío con ilustración cuando no hay tareas en el filtro activo

---

## `TaskDetailModal`

**Archivo**: [src/features/task/components/TaskDetailModal.jsx](../../src/features/task/components/TaskDetailModal.jsx)

Modal que muestra el detalle completo de una tarea y permite editarla o eliminarla.

```jsx
<TaskDetailModal
  task={selectedTask}
  onClose={() => setSelected(null)}
  onStatusChange={(taskId, status) => updateStatus(taskId, status)}
  onDelete={(taskId) => deleteTask(taskId)}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `task` | `Task \| null` | Tarea a mostrar (null = cerrado) |
| `onClose` | `() => void` | Callback para cerrar el modal |
| `onStatusChange` | `(taskId, status) => void` | Callback para cambiar estado |
| `onDelete` | `(taskId) => void` | Callback para eliminar tarea |

**Campos mostrados**:
- Título
- Estado actual con selector desplegable
- Prioridad (alta / media / baja)
- Fecha de vencimiento
- Duración estimada en minutos
- Botón de eliminar con confirmación

---

## `CreateTaskPanel`

**Archivo**: [src/features/task/components/CreateTaskPanel.jsx](../../src/features/task/components/CreateTaskPanel.jsx)

Panel lateral deslizante con el formulario para crear una nueva tarea. Se cierra al guardar correctamente o al cancelar.

```jsx
<CreateTaskPanel
  isOpen={panelOpen}
  onClose={() => setPanelOpen(false)}
  onSubmit={(data) => createTask(data)}
  loading={creating}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `isOpen` | `boolean` | Controla visibilidad del panel |
| `onClose` | `() => void` | Callback para cerrar |
| `onSubmit` | `(data: TaskInput) => Promise<void>` | Callback de envío del formulario |
| `loading` | `boolean` | Deshabilita el botón mientras crea |

**Campos del formulario**:

| Campo | Tipo | Requerido |
|-------|------|-----------|
| Título | text | Sí |
| Fecha de vencimiento | date | Sí |
| Prioridad | select (alta/media/baja) | Sí |
| Duración estimada | number (min) | No |

---

## `SidePanel`

**Archivo**: [src/features/task/components/SidePanel.jsx](../../src/features/task/components/SidePanel.jsx)

Wrapper genérico para paneles laterales con animación slide-in/out. Puede reutilizarse en otras features.

```jsx
<SidePanel isOpen={open} onClose={close} title="Título del panel">
  {/* contenido */}
</SidePanel>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `isOpen` | `boolean` | Controla la visibilidad |
| `onClose` | `() => void` | Callback para cerrar |
| `title` | `string` | Título del header del panel |
| `children` | `ReactNode` | Contenido interior |

Incluye overlay oscuro en el fondo que también cierra el panel al hacer clic.

---

## `Modal`

**Archivo**: [src/features/task/components/Modal.jsx](../../src/features/task/components/Modal.jsx)

Componente modal genérico centrado en pantalla. Puede usarse para confirmaciones, detalles o formularios.

```jsx
<Modal isOpen={open} onClose={close} title="Confirmar acción">
  <p>¿Estás seguro?</p>
  <button onClick={confirm}>Confirmar</button>
</Modal>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `isOpen` | `boolean` | Controla la visibilidad |
| `onClose` | `() => void` | Callback para cerrar |
| `title` | `string?` | Título del header |
| `children` | `ReactNode` | Contenido del modal |

Cierra al hacer clic en el overlay o presionar `Escape`.
