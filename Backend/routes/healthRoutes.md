# src/routes/healthRoutes.js

Router de diagnóstico del servidor. Define los endpoints de salud sin requerir autenticación.

## Rutas

| Método | Ruta           | Auth | Controlador                   | Descripción                           |
|--------|----------------|------|-------------------------------|---------------------------------------|
| `GET`  | `/hola-mundo`  | No   | `healthController.getHelloWorld` | Prueba de conexión a la base de datos. |
| `GET`  | `/health`      | No   | `healthController.getHealth`     | Estado completo del servidor.          |

Este router se monta bajo el prefijo `/api` en `app.js`, por lo que las rutas completas son:
- `GET /api/hola-mundo`
- `GET /api/health`

## Dependencias

- `express`
- `../controllers/healthController`
