# src/pages/TaskPage.jsx

Proposito
- Pagina de tareas con layout tipo tabla.

Responsabilidades
- Renderizar encabezado de columnas.
- Consumir `useTasks` y renderizar `TaskList`.
- Mantener el scroll dentro del listado.

Flujo basico
1) Ejecutar `useTasks` al montar.
2) Mostrar encabezados.
3) Renderizar `TaskList` con los datos.

Entradas/Salidas
- Entradas: estado del hook `useTasks`.
- Salidas: UI de listado de tareas.

Dependencias
- ../features/task/hooks/useTasks
- ../features/task/components/TaskList

Notas
- El scroll esta contenido dentro del listado.

Ejemplo
```js
// <TaskPage />
```
