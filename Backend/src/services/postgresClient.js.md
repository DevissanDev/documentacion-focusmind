# src/services/postgresClient.js

Proposito
- Configurar el pool de Postgres.
- Exponer utilidad de prueba de conexion.

Responsabilidades
- Crear instancia de `Pool` con envs.
- Ejecutar `SELECT NOW()` para test.

Flujo basico
1) Leer variables de entorno.
2) Crear `Pool`.
3) Exportar `pool` y `testConnection`.

Entradas/Salidas
- Entradas: `PGHOST`, `PGPORT`, `PGDATABASE`, `PGUSER`, `PGPASSWORD`, `PGSSL`.
- Salidas: pool activo y resultado de prueba.

Dependencias
- pg

Notas
- Si `PGSSL` es `true`, usa SSL sin validar certificado.

Ejemplo
```js
// const { pool } = require("./postgresClient");
```
