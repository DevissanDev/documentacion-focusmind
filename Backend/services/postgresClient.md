# src/services/postgresClient.js

Cliente de base de datos PostgreSQL. Crea y exporta el pool de conexiones compartido por todos los servicios de la aplicación.

## Pool de conexiones

Se inicializa una instancia de `pg.Pool` con los siguientes parámetros tomados de variables de entorno:

| Variable de entorno | Descripción                                      | Defecto |
|---------------------|--------------------------------------------------|---------|
| `PGHOST`            | Host del servidor PostgreSQL.                    | —       |
| `PGPORT`            | Puerto del servidor PostgreSQL.                  | `5432`  |
| `PGDATABASE`        | Nombre de la base de datos.                      | —       |
| `PGUSER`            | Usuario de la base de datos.                     | —       |
| `PGPASSWORD`        | Contraseña del usuario.                          | —       |
| `PGSSL`             | Si es `"true"`, activa SSL con `rejectUnauthorized: false`. | `false` |

## Exportaciones

### `pool`

Instancia de `pg.Pool`. Todos los servicios la importan para ejecutar queries mediante `pool.query(sql, params)`.

### `testConnection()`

Función asíncrona que ejecuta `SELECT NOW()` para verificar la conectividad.

**Retorna:**

```json
// Éxito
{ "success": true, "message": "conexion correcta", "timestamp": { "now": "<datetime>" } }

// Error
{ "success": false, "message": "Error en la conexion", "error": "<mensaje de error>" }
```

## Dependencias

- `pg` (node-postgres)
