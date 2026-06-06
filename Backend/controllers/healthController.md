# src/controllers/healthController.js

Controlador de diagnóstico del servidor. Expone dos endpoints para verificar que la API y la base de datos están operativas.

## Funciones exportadas

### `getHelloWorld(req, res)`

Prueba directa de conectividad con la base de datos.

- Llama a `testConnection()` del cliente PostgreSQL.
- Devuelve `200 { message: "conexion correcta" }` si la conexión es exitosa.
- Devuelve `500 { message: "Error en la conexion", error }` si falla.

**Ruta asociada:** `GET /`

---

### `getHealth(req, res)`

Estado detallado del servidor.

- Llama a `healthService.getHealthStatus()`.
- Devuelve `200` con el objeto de estado que incluye `status`, `timestamp` y estado de la base de datos.
- Devuelve `500` con mensaje de error si el servicio falla.

**Ruta asociada:** `GET /api/health`

## Dependencias

- `../services/healthService`
- `../services/postgresClient` (función `testConnection`)
