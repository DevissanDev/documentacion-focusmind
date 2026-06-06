# Feature: Dashboard

Página principal de analíticas. Visualiza tendencias del bienestar emocional, progreso de tareas semanales y carga cognitiva anual del usuario mediante tres gráficos interactivos.

## Archivos relevantes

```
src/features/dashboard/
├── components/
│   ├── EmotionalDistributionChart.jsx  # Gráfico de distribución emocional
│   ├── WeeklyTasksChart.jsx            # Gráfico de tareas semanales
│   └── CognitiveTrendChart.jsx         # Gráfico de tendencia cognitiva anual
├── hooks/
│   ├── useEmotionalDistribution.js
│   ├── useWeeklyTasks.js
│   └── useCognitiveTrend.js
└── services/
    └── chartsApi.js                    # Llamadas a la API de gráficos
```

```
src/pages/DashboardPage.jsx             # Página que ensambla los tres gráficos
```

## API

Base path: `/charts`

| Función | Método | Endpoint | Descripción |
|---------|--------|----------|-------------|
| `fetchEmotionalDistribution(userId, month, year)` | GET | `/charts/:userId/emotional-distribution?month=&year=` | Distribución de estados emocionales en el mes |
| `fetchWeeklyTasks(userId, month, year)` | GET | `/charts/:userId/weekly-tasks?month=&year=` | Progreso de tareas por semana del mes |
| `fetchCognitiveTrend(userId, year)` | GET | `/charts/:userId/cognitive-trend?year=` | Tendencia de carga cognitiva mensual del año |

### Respuesta `fetchEmotionalDistribution`

```json
{
  "data": [
    { "state": "Excelente", "count": 8 },
    { "state": "Bien", "count": 12 },
    { "state": "Neutral", "count": 5 },
    { "state": "Mal", "count": 3 },
    { "state": "Muy Mal", "count": 1 }
  ]
}
```

### Respuesta `fetchWeeklyTasks`

```json
{
  "weeks": [
    { "label": "Semana 1", "completed": 7, "total": 10 },
    { "label": "Semana 2", "completed": 4, "total": 8 }
  ]
}
```

### Respuesta `fetchCognitiveTrend`

```json
{
  "months": [
    { "month": "Ene", "score": 65 },
    { "month": "Feb", "score": 72 }
  ]
}
```

## Hooks

### `useEmotionalDistribution(userId, month, year)`

Carga la distribución de estados emocionales del mes. Retorna `{ data, loading, error }`.

### `useWeeklyTasks(userId, month, year)`

Carga el progreso de tareas por semana del mes. Retorna `{ weeks, loading, error }`.

### `useCognitiveTrend(userId, year)`

Carga la tendencia de carga cognitiva mensual del año. Retorna `{ months, loading, error }`.

## Componentes

### `EmotionalDistributionChart`

Gráfico de pastel o barras que muestra el porcentaje de cada estado emocional en el mes seleccionado. Cada emoción tiene un color diferenciado.

**Librería**: `@mui/x-charts`

**Controles**: selector de mes y año.

### `WeeklyTasksChart`

Gráfico de barras agrupadas que compara tareas completadas vs. total por semana del mes.

**Librería**: `@mui/x-charts`

**Controles**: selector de mes y año.

### `CognitiveTrendChart`

Gráfico de línea que muestra la evolución mensual de la carga cognitiva a lo largo del año.

**Librería**: `@mui/x-charts`

**Controles**: selector de año.

## Ruta

`/dashboard` — es la ruta de inicio al autenticarse. Renderizada en `DashboardPage` dentro del `DashboardShell`.

## Relación con otras features

- Los datos de **Registro Emocional** alimentan `EmotionalDistributionChart`
- Los datos de **Tareas** alimentan `WeeklyTasksChart`
- Los datos de **Calendario** (carga cognitiva) alimentan `CognitiveTrendChart`
