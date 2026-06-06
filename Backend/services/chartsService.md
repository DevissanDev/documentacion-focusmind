# src/services/chartsService.js

Servicio de datos para gráficas analíticas. Ejecuta las consultas SQL necesarias para construir datasets de tipo pie, bar y line.

## Funciones exportadas

### `getEmotionalDistribution({ userId, month, year })`

Cuenta el número de registros emocionales agrupados por estado para un mes y año dados.

**SQL:** `JOIN emotional_records + emotional_states`, filtra por `user_id`, `MONTH` y `YEAR`, agrupa por estado.

**Retorna:**
```json
{
  "period": "2025-01",
  "labels": ["Feliz", "Triste", "Ansioso"],
  "data": [5, 3, 2],
  "total": 10,
  "chart_type": "pie"
}
```

---

### `getWeeklyTaskProgress({ userId, month, year })`

Calcula el progreso de tareas agrupado por semana del mes (semanas 1-4). Semanas sin tareas se rellenan con ceros.

**SQL:** Agrupa por `LEAST(CEIL(DAY/7), 4)` para asignar cada día a una de las 4 semanas del mes.

**Retorna:**
```json
{
  "period": "2025-01",
  "labels": ["Semana 1", "Semana 2", "Semana 3", "Semana 4"],
  "done": [3, 5, 2, 4],
  "pending": [1, 0, 3, 2],
  "chart_type": "bar"
}
```

---

### `getCognitiveTrend({ userId, year })`

Calcula el promedio de carga cognitiva mensual durante un año completo. Meses sin registros devuelven `null` en `values` y `0` en `records_counts`.

**Fórmula de carga cognitiva:**
```
carga = 100 - (emotional_state_id - 1) * (99.0 / 4)
```
Un estado con ID 1 produce 100 (máxima energía), ID 5 produce ~1 (mínima energía).

**Retorna:**
```json
{
  "year": 2025,
  "labels": ["Enero", "Febrero", ..., "Diciembre"],
  "values": [85.5, null, 72.0, ...],
  "records_counts": [10, 0, 8, ...],
  "chart_type": "line"
}
```

## Dependencias

- `./postgresClient` (instancia `pool`)
