# Feature: Registro Emocional

Permite al usuario registrar y consultar su estado emocional a lo largo del tiempo. Los registros son la base de datos que alimenta el calendario y los gráficos del dashboard.

## Archivos relevantes

```
src/features/registroEmocional/
├── components/
│   └── RegistroEmocionalList.jsx   # Lista + formulario de registro emocional
├── hooks/
│   └── useRegistroEmocional.js     # Estado y operaciones
└── services/
    └── registroEmocionalApi.js     # Llamadas a la API
```

```
src/pages/RegistroEmocionalPage.jsx  # Página que ensambla la feature
src/assets/                          # Imágenes de emociones (emojis)
```

## Estados emocionales

| ID | Etiqueta | Imagen |
|----|---------|--------|
| 1 | Excelente | `sonrisa.png` |
| 2 | Bien | `corazones.png` |
| 3 | Neutral | `meh.png` |
| 4 | Mal | `triste.png` |
| 5 | Muy Mal | `enfadado.png` |

## API

Base path: `/emotionalrecords`

| Función | Método | Endpoint | Descripción |
|---------|--------|----------|-------------|
| `fetchEmotionalRecords(userId, date?, stateId?)` | GET | `/emotionalrecords/:userId/list` | Obtener registros con filtros opcionales |
| `submitEmotionalRecord(userId, payload)` | POST | `/emotionalrecords/:userId/create` | Crear nuevo registro emocional |

### Query params de `fetchEmotionalRecords`

| Parámetro | Tipo | Descripción |
|-----------|------|-------------|
| `date` | `YYYY-MM-DD` | Filtrar por fecha específica |
| `stateId` | `number` | Filtrar por ID de estado emocional |

Ambos parámetros son opcionales. Se omiten del query string si no se proporcionan.

### Payload de creación

```json
{
  "stateId": 1,
  "notes": "string (opcional)",
  "timestamp": "ISO 8601"
}
```

## Hook: `useRegistroEmocional`

```js
const {
  records,         // EmotionalRecord[]
  loading,         // boolean
  error,           // string | null
  submitRecord,    // (stateId, notes?) => Promise<void>
  filterByDate,    // (date: string) => void
  filterByState,   // (stateId: number) => void
  refetch,         // () => Promise<void>
} = useRegistroEmocional()
```

## Componente: `RegistroEmocionalList`

Componente principal de la feature. Combina:
- **Lista de registros**: muestra cada registro con emoji, etiqueta, fecha y notas
- **Formulario de nuevo registro**: selector de estado emocional con emojis clickeables
- **Filtros**: por fecha y por tipo de emoción
- **Estado vacío**: mensaje cuando no hay registros para los filtros activos

Los emojis se renderizan usando las imágenes de `/src/assets/` para una UX visual y accesible.

## Ruta

`/registro-emocional` — renderizada en `RegistroEmocionalPage` dentro del `DashboardShell`.

## Relación con otras features

- **Calendario**: consume los mismos registros para colorear los días del mes según el estado emocional
- **Dashboard**: usa los datos agregados para el gráfico de distribución emocional (`EmotionalDistributionChart`)
