# app.js

Punto de entrada de la aplicación Express. Configura el servidor, registra los middlewares globales y monta todos los routers.

## Responsabilidades

- Inicializa la instancia de Express.
- Aplica `cors()` para permitir peticiones desde cualquier origen.
- Aplica `express.json()` para parsear cuerpos de petición en JSON.
- Registra la ruta raíz `GET /` directamente con `healthController.getHelloWorld`.
- Monta los routers de la aplicación:

| Prefijo | Router                    |
|---------|---------------------------|
| `/api`  | `healthRoutes`            |
| `/api`  | `emotionalRecordsRoutes`  |
| `/`     | `emotionalRecordsRoutes`  |
| `/`     | `tasksRoutes`             |
| `/`     | `chartsRoutes`            |

> `emotionalRecordsRoutes` se monta dos veces: bajo `/api` y bajo `/` para cubrir tanto rutas con prefijo como sin él.

## Exportaciones

| Nombre | Tipo     | Descripción                               |
|--------|----------|-------------------------------------------|
| `app`  | `object` | Instancia de Express lista para escuchar. |

## Dependencias

- `express`
- `cors`
- `./src/routes/healthRoutes`
- `./src/controllers/healthController`
- `./src/routes/emotionalRecordsRoutes`
- `./src/routes/tasksRoutes`
- `./src/routes/chartsRoutes`
