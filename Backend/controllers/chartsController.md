# src/controllers/chartsController.js

Controlador para los endpoints de gráficas analíticas del usuario. Valida los parámetros de entrada y delega el cálculo de datos al servicio `chartsService`.

## Funciones exportadas

### `getEmotionalDistribution(req, res)`

Distribución de estados emocionales en un mes/año para construir una gráfica de tipo **pie**.

**Parámetros de ruta:** `userId`  
**Query params:** `month` (1-12), `year` (≥ 2000)

- Valida presencia y rango de `month` y `year`; devuelve `400` si son inválidos.
- Llama a `chartsService.getEmotionalDistribution({ userId, month, year })`.
- Devuelve `200` con `{ period, labels, data, total, chart_type: "pie" }`.

**Ruta asociada:** `GET /charts/:userId/emotional-distribution`

---

### `getWeeklyTaskProgress(req, res)`

Progreso semanal de tareas en un mes/año para construir una gráfica de tipo **bar**.

**Parámetros de ruta:** `userId`  
**Query params:** `month` (1-12), `year` (≥ 2000)

- Misma validación que `getEmotionalDistribution`.
- Llama a `chartsService.getWeeklyTaskProgress({ userId, month, year })`.
- Devuelve `200` con `{ period, labels, done, pending, chart_type: "bar" }`.

**Ruta asociada:** `GET /charts/:userId/weekly-tasks`

---

### `getCognitiveTrend(req, res)`

Tendencia anual de carga cognitiva para construir una gráfica de tipo **line**.

**Parámetros de ruta:** `userId`  
**Query params:** `year` (≥ 2000; por defecto: año actual)

- Valida que `year` sea un entero ≥ 2000; devuelve `400` si no lo es.
- Llama a `chartsService.getCognitiveTrend({ userId, year })`.
- Devuelve `200` con `{ year, labels, values, records_counts, chart_type: "line" }`.

**Ruta asociada:** `GET /charts/:userId/cognitive-trend`

## Códigos de respuesta comunes

| Código | Descripción                          |
|--------|--------------------------------------|
| `200`  | Datos obtenidos correctamente.       |
| `400`  | Parámetros faltantes o inválidos.    |
| `500`  | Error interno al consultar el servicio. |

## Dependencias

- `../services/chartsService`
