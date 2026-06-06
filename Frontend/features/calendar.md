# Feature: Calendario

Visualización mensual interactiva que combina el estado emocional de cada día con las tareas vencidas. Incluye un indicador de carga cognitiva y un panel de resumen diario al seleccionar un día.

## Archivos relevantes

```
src/features/calendar/
├── Calendar.jsx               # Componente raíz de la feature
├── components/
│   ├── CalendarPage.jsx       # Wrapper de página
│   ├── CognitiveLoadGauge.jsx # Medidor de carga cognitiva
│   ├── DailySummaryCard.jsx   # Resumen del día seleccionado
│   ├── FocusModeButton.jsx    # Botón para activar modo enfoque
│   ├── FocusModePopup.jsx     # Popup del modo enfoque
│   └── TodayEmotionPanel.jsx  # Panel de emoción del día actual
├── hooks/
│   ├── useCalendarData.js     # Datos mensuales del calendario
│   ├── useCognitiveLoad.js    # Carga cognitiva del mes
│   └── useDailySummary.js     # Resumen de un día específico
└── services/
    └── calendarApi.js         # Llamadas a la API del calendario
```

```
src/pages/CalendarPage.jsx     # Página que ensambla la feature
```

## API

| Función | Método | Endpoint | Descripción |
|---------|--------|----------|-------------|
| `fetchCalendarMonth(userId, month, year)` | GET | `/:monthName/:userId?year=` | Datos del mes (emociones + tareas por día) |
| `fetchDailySummary(userId, date)` | GET | `/summary/:userId?date=` | Detalle de un día específico |
| `fetchCognitiveLoad(userId, month, year)` | GET | `/cognitive-load/:userId?month=&year=` | Carga cognitiva del mes |

El endpoint de mes usa el nombre del mes en español (ej: `enero`, `febrero`) en lugar del número.

### Respuesta de `fetchCalendarMonth`

```json
{
  "days": [
    {
      "date": "YYYY-MM-DD",
      "emotionalState": { "id": 1, "label": "Excelente" },
      "overdueTasks": 2
    }
  ]
}
```

### Respuesta de `fetchCognitiveLoad`

```json
{
  "score": 72,
  "level": "alta | media | baja"
}
```

## Hooks

### `useCalendarData(userId, month, year)`

Carga los datos del mes completo. Retorna el array de días con sus estados emocionales y tareas vencidas.

### `useCognitiveLoad(userId, month, year)`

Retorna el score de carga cognitiva del mes seleccionado. Es el dato que alimenta `CognitiveLoadGauge`.

### `useDailySummary(userId, date)`

Carga el detalle de un día al hacer clic en él. Alimenta `DailySummaryCard`.

## Componentes

### `Calendar` (raíz)

Renderiza la cuadrícula del mes. Cada celda muestra:
- Un indicador de color según el estado emocional del día
- Un badge con el número de tareas vencidas (si hay)
- Estado activo al seleccionar un día

Expone un callback `onDaySelect` para comunicar el día seleccionado a los paneles laterales.

### `CognitiveLoadGauge`

Medidor visual (gauge) que muestra el nivel de carga cognitiva del mes actual. Recibe `score` (0–100) y muestra el nivel textual.

### `DailySummaryCard`

Panel que se activa al seleccionar un día. Muestra:
- Estado emocional del día
- Lista de tareas del día (completadas vs. pendientes)
- Notas del registro emocional (si las hay)

### `TodayEmotionPanel`

Muestra el estado emocional registrado hoy. Si no hay registro, invita al usuario a registrar su emoción del día.

### `FocusModeButton` / `FocusModePopup`

Botón en la interfaz del calendario que abre un popup con el modo de concentración. Permite activar una sesión de foco desde la vista de calendario.

## Ruta

`/calendario` — renderizada en `CalendarPage` dentro del `DashboardShell`.

## Relación con otras features

- Consume los mismos datos que **Registro Emocional** para colorear los días
- Muestra tareas vencidas calculadas desde **Tareas**
- El `FocusModePopup` es el punto de entrada a la feature **Concentration**
