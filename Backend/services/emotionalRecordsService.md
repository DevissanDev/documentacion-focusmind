# src/services/emotionalRecordsService.js

Servicio para la gestión de registros emocionales. Encapsula todas las consultas SQL relacionadas con emociones, resúmenes mensuales y carga cognitiva.

## Funciones exportadas

### `listEmotionalRecordsByUser(userId, date, stateId)`

Lista los registros emocionales de un usuario con filtros opcionales de fecha y estado.

**SQL:** `JOIN emotional_records + emotional_states`. Filtra con parámetros nulables:
- `$2::date IS NULL OR created_at::date = $2`
- `$3::integer IS NULL OR emotional_state_id = $3`

**Retorna:** Array de `{ id, user_id, emotional_state_id, name, created_at }` ordenado por fecha descendente.

---

### `createEmotionalRecord(userId, emotionalStateId)`

Inserta un nuevo registro emocional y retorna el registro creado con el nombre del estado.

**SQL:** CTE con `INSERT INTO emotional_records ... RETURNING` + `JOIN emotional_states`.

**Retorna:** `{ id, user_id, emotional_state_id, name, created_at }`

---

### `getMonthlySummaryByUser({ userId, month, year })`

Genera un resumen día a día del mes completo, incluyendo estados emocionales registrados y número de tareas con vencimiento ese día.

**SQL:** Three-CTE query:
1. `days` — genera todas las fechas del mes con `generate_series`.
2. `latest_emotional` — agrupa estados emocionales por día (`ARRAY_AGG`).
3. `tasks_due` — cuenta tareas con `due_date` en ese día.

Los tres se unen con `LEFT JOIN` para garantizar que todos los días del mes aparezcan aunque no tengan datos.

**Retorna:** Array de objetos por cada día del mes:
```json
[
  {
    "date": "2025-01-01",
    "emotional_states": ["Feliz", "Tranquilo"],
    "tasks_due_count": 3
  }
]
```

---

### `getMonthlyCognitiveLoadByUser({ userId, month, year })`

Calcula la carga cognitiva promedio del usuario para un mes completo.

**Fórmula:** `100 - (emotional_state_id - 1) * (99.0 / 4)` — mapea el ID del estado a un valor 1-100.

**Retorna:**
```json
{
  "month": "2025-01",
  "average_cognitive_load": "72.50",
  "records_count": 8
}
```

## Función auxiliar interna

### `monthNameToNumber(month)`

Convierte un nombre de mes en español (o un número como string) a su número entero (1-12).

| Entrada          | Salida |
|------------------|--------|
| `"enero"`        | `1`    |
| `"septiembre"` / `"setiembre"` | `9` |
| `"12"` / `12`    | `12`   |
| Valor inválido   | `null` |

## Dependencias

- `./postgresClient` (instancia `pool`)
