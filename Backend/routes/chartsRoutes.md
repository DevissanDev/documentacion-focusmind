# src/routes/chartsRoutes.js

Router para los endpoints de gráficas analíticas. Todas las rutas requieren autenticación Cognito.

## Rutas

| Método | Ruta                                      | Auth    | Controlador                                 | Descripción                                    |
|--------|-------------------------------------------|---------|---------------------------------------------|------------------------------------------------|
| `GET`  | `/charts/:userId/emotional-distribution`  | Cognito | `chartsController.getEmotionalDistribution` | Distribución de estados emocionales (pie chart). |
| `GET`  | `/charts/:userId/weekly-tasks`            | Cognito | `chartsController.getWeeklyTaskProgress`    | Progreso semanal de tareas (bar chart).         |
| `GET`  | `/charts/:userId/cognitive-trend`         | Cognito | `chartsController.getCognitiveTrend`        | Tendencia anual de carga cognitiva (line chart). |

Este router se monta bajo el prefijo `/` en `app.js`.

## Query params comunes

| Endpoint                    | Params requeridos              |
|-----------------------------|-------------------------------|
| `emotional-distribution`    | `month` (1-12), `year` (YYYY) |
| `weekly-tasks`              | `month` (1-12), `year` (YYYY) |
| `cognitive-trend`           | `year` (YYYY, opcional)       |

## Dependencias

- `express`
- `../controllers/chartsController`
- `../middlewares/cognitoAuth`
