# Componentes: Calendario

Componentes que conforman la página del calendario (`/calendario`). Viven en `src/features/calendar/components/`.

---

## `Calendar` (raíz)

**Archivo**: [src/features/calendar/Calendar.jsx](../../src/features/calendar/Calendar.jsx)

Cuadrícula del mes con navegación entre meses. Cada celda del día muestra:
- Color de fondo según el estado emocional registrado ese día
- Badge numérico con tareas vencidas (si las hay)
- Borde destacado para el día seleccionado

```jsx
<Calendar
  userId={userId}
  onDaySelect={(date) => setSelectedDate(date)}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `userId` | `string` | ID del usuario autenticado |
| `onDaySelect` | `(date: string) => void` | Callback al hacer clic en un día |

**Internamente** usa `useCalendarData` para obtener los datos del mes y `useCognitiveLoad` para el score mensual.

---

## `CognitiveLoadGauge`

**Archivo**: [src/features/calendar/components/CognitiveLoadGauge.jsx](../../src/features/calendar/components/CognitiveLoadGauge.jsx)

Indicador visual semicircular (gauge) que muestra el nivel de carga cognitiva del mes actual.

```jsx
<CognitiveLoadGauge score={72} level="alta" />
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `score` | `number` | Valor de 0 a 100 |
| `level` | `"baja" \| "media" \| "alta"` | Nivel textual del score |

Los colores cambian según el nivel:
- **Baja** (0–40): verde
- **Media** (41–70): amarillo/ámbar
- **Alta** (71–100): rojo

---

## `DailySummaryCard`

**Archivo**: [src/features/calendar/components/DailySummaryCard.jsx](../../src/features/calendar/components/DailySummaryCard.jsx)

Tarjeta lateral que se activa al seleccionar un día en el calendario. Muestra el resumen del día.

```jsx
<DailySummaryCard
  userId={userId}
  date="2026-06-06"
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `userId` | `string` | ID del usuario |
| `date` | `string` | Fecha en formato `YYYY-MM-DD` |

**Contenido mostrado**:
- Estado emocional del día con emoji
- Lista de tareas del día (completadas y pendientes)
- Notas del registro emocional
- Indicador de carga mientras carga (`useDailySummary`)

Muestra un mensaje de placeholder cuando `date` es `null` (sin día seleccionado).

---

## `TodayEmotionPanel`

**Archivo**: [src/features/calendar/components/TodayEmotionPanel.jsx](../../src/features/calendar/components/TodayEmotionPanel.jsx)

Panel que muestra el estado emocional registrado hoy. Si no hay registro del día de hoy, muestra un CTA para ir a `/registro-emocional`.

```jsx
<TodayEmotionPanel userId={userId} />
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `userId` | `string` | ID del usuario |

---

## `FocusModeButton`

**Archivo**: [src/features/calendar/components/FocusModeButton.jsx](../../src/features/calendar/components/FocusModeButton.jsx)

Botón flotante o inline que abre el popup del modo enfoque. Recibe el estado de visibilidad del popup.

```jsx
<FocusModeButton onClick={() => setPopupOpen(true)} />
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `onClick` | `() => void` | Callback para abrir el popup |

---

## `FocusModePopup`

**Archivo**: [src/features/calendar/components/FocusModePopup.jsx](../../src/features/calendar/components/FocusModePopup.jsx)

Modal/popup con la interfaz del modo de concentración. Permite al usuario iniciar una sesión de trabajo enfocado.

```jsx
<FocusModePopup
  isOpen={popupOpen}
  onClose={() => setPopupOpen(false)}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `isOpen` | `boolean` | Visibilidad del popup |
| `onClose` | `() => void` | Callback para cerrar |

**Contenido**: timer de sesión de foco, opciones de duración, indicador de progreso.
