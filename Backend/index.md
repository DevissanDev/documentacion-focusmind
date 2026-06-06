# Documentación — med-core

API REST para la gestión de salud y bienestar emocional. Construida con Node.js, Express y PostgreSQL, autenticada con AWS Cognito.

## Estructura

```
med-core/
├── server.js                        # Arranque del servidor HTTP
├── app.js                           # Configuración Express y montaje de rutas
└── src/
    ├── middlewares/
    │   └── cognitoAuth.js           # Verificación de JWT de AWS Cognito
    ├── routes/
    │   ├── healthRoutes.js          # GET /api/hola-mundo, GET /api/health
    │   ├── emotionalRecordsRoutes.js# Rutas de registros emocionales
    │   ├── tasksRoutes.js           # Rutas de tareas
    │   └── chartsRoutes.js          # Rutas de gráficas analíticas
    ├── controllers/
    │   ├── healthController.js      # Diagnóstico del servidor
    │   ├── emotionalRecordsController.js # Lógica HTTP de emociones
    │   ├── tasksController.js       # Lógica HTTP de tareas
    │   └── chartsController.js      # Lógica HTTP de gráficas
    └── services/
        ├── postgresClient.js        # Pool de conexiones PostgreSQL
        ├── healthService.js         # Estado del servidor
        ├── emotionalRecordsService.js # Queries de registros emocionales
        ├── tasksService.js          # Queries de tareas
        └── chartsService.js         # Queries de datos para gráficas
```

## Índice de archivos documentados

### Raíz
- [server.js](server.md) — Arranque del servidor, carga `.env`, escucha en `PORT`.
- [app.js](app.md) — Instancia Express, CORS, JSON parser, montaje de routers.

### Middlewares
- [cognitoAuth.js](middlewares/cognitoAuth.md) — Validación de Bearer JWT contra AWS Cognito.

### Routes
- [healthRoutes.js](routes/healthRoutes.md) — Endpoints de diagnóstico (sin auth).
- [emotionalRecordsRoutes.js](routes/emotionalRecordsRoutes.md) — Listado, creación y resúmenes emocionales.
- [tasksRoutes.js](routes/tasksRoutes.md) — CRUD de tareas y resumen diario.
- [chartsRoutes.js](routes/chartsRoutes.md) — Datos para gráficas pie, bar y line.

### Controllers
- [healthController.js](controllers/healthController.md) — `getHelloWorld`, `getHealth`.
- [emotionalRecordsController.js](controllers/emotionalRecordsController.md) — `listByUser`, `createForUser`, `getMonthlySummaryByUser`, `getMonthlyCognitiveLoadByUser`.
- [tasksController.js](controllers/tasksController.md) — `listByUser`, `create`, `updateStatus`, `remove`, `getDailySummary`.
- [chartsController.js](controllers/chartsController.md) — `getEmotionalDistribution`, `getWeeklyTaskProgress`, `getCognitiveTrend`.

### Services
- [postgresClient.js](services/postgresClient.md) — Pool `pg` y función `testConnection`.
- [healthService.js](services/healthService.md) — `getHealthStatus`.
- [emotionalRecordsService.js](services/emotionalRecordsService.md) — Queries de registros emocionales y carga cognitiva.
- [tasksService.js](services/tasksService.md) — CRUD de tareas y resumen diario por SQL.
- [chartsService.js](services/chartsService.md) — Queries para distribución emocional, progreso semanal y tendencia cognitiva.

## Variables de entorno requeridas

| Variable                     | Descripción                                     |
|------------------------------|-------------------------------------------------|
| `PORT`                       | Puerto HTTP (defecto: 3000).                    |
| `PGHOST`                     | Host PostgreSQL.                                |
| `PGPORT`                     | Puerto PostgreSQL (defecto: 5432).              |
| `PGDATABASE`                 | Nombre de la base de datos.                     |
| `PGUSER`                     | Usuario PostgreSQL.                             |
| `PGPASSWORD`                 | Contraseña PostgreSQL.                          |
| `PGSSL`                      | `"true"` para habilitar SSL.                    |
| `COGNITO_REGION`             | Región AWS del User Pool.                       |
| `COGNITO_USER_POOL_ID`       | ID del User Pool de Cognito.                    |
| `COGNITO_CLIENT_ID`          | ID del cliente de aplicación Cognito.           |
| `COGNITO_TOKEN_USE`          | `access` (defecto) o `id`.                      |
| `COGNITO_ENFORCE_USER_MATCH` | `"true"` (defecto) valida sub == userId.        |

## Flujo de una petición autenticada

```
Cliente
  → Authorization: Bearer <JWT>
  → Route Handler
  → cognitoAuth middleware (verifica JWT contra JWKS de Cognito)
  → Controller (valida params HTTP)
  → Service (ejecuta SQL con pool de pg)
  → Respuesta JSON
```
