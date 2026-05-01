# src/features/task/components/TaskList.jsx

Proposito
- UI del listado de tareas.

Responsabilidades
- Renderizar estados de carga, error y vacio.
- Normalizar campos comunes del API.
- Mostrar filas con titulo, estado, fecha, tiempo y prioridad.

Flujo basico
1) Mostrar loader o mensaje de error.
2) Renderizar estado vacio si no hay datos.
3) Renderizar filas con los campos normalizados.

Entradas/Salidas
- Entradas: props con `tasks`, `loading`, `error`.
- Salidas: tabla/listado renderizado.

Dependencias
- React

Notas
- Normaliza campos del API para la UI.

Ejemplo
```js
// <TaskList tasks={tasks} loading={loading} error={error} />
```
