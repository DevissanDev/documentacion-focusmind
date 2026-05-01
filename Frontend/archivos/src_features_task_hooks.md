# src/features/task/hooks/useTasks.js

Proposito
- Hook de carga para tareas.

Responsabilidades
- Resolver `userId` con Amplify.
- Gestionar `tasks`, `loading` y `error`.
- Invocar `taskApi`.

Flujo basico
1) Obtener `userId` de la sesion.
2) Llamar a `taskApi`.
3) Actualizar estado local.

Entradas/Salidas
- Entradas: sesion de usuario.
- Salidas: `{ tasks, loading, error }`.

Dependencias
- ../../services/taskApi
- aws-amplify

Notas
- Maneja estado de carga y error para UI.

Ejemplo
```js
// const { tasks, loading, error } = useTasks();
```
