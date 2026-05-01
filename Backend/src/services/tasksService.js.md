# src/services/tasksService.js

Proposito
- Consultar tareas en Postgres.
- Entregar datos listos para el controlador.

Responsabilidades
- Ejecutar query parametrizado por usuario.
- Ordenar por fecha de creacion descendente.

Flujo basico
1) Construir SQL parametrizado.
2) Ejecutar `pool.query`.
3) Retornar `rows`.

Entradas/Salidas
- Entradas: `userId`.
- Salidas: array de tareas.

Dependencias
- ./postgresClient

Notas
- Retorna todas las columnas definidas en `tasks`.

Ejemplo
```js
// const rows = await listTasksByUser("123");
```
