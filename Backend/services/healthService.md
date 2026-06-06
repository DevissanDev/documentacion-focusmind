# src/services/healthService.js

Servicio de diagnóstico del servidor. Comprueba la conectividad con la base de datos y retorna un objeto de estado.

## Funciones exportadas

### `getHealthStatus()`

Función asíncrona que retorna el estado actual del servidor y de la base de datos.

**Retorna:**

```json
// Base de datos conectada
{
  "status": "ok",
  "timestamp": "2025-01-15T12:00:00.000Z",
  "database": "connected"
}

// Base de datos con error
{
  "status": "ok",
  "timestamp": "2025-01-15T12:00:00.000Z",
  "database": "error",
  "databaseError": "<mensaje de error>"
}
```

| Campo           | Tipo     | Descripción                                         |
|-----------------|----------|-----------------------------------------------------|
| `status`        | `string` | Siempre `"ok"` (el servicio HTTP responde).         |
| `timestamp`     | `string` | Fecha y hora ISO 8601 del momento de la consulta.   |
| `database`      | `string` | `"connected"` si la BD responde, `"error"` si falla. |
| `databaseError` | `string` | Presente solo si `database === "error"`.            |

## Dependencias

- `./postgresClient` (función `testConnection`)
