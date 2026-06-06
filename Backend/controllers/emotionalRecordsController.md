# src/controllers/emotionalRecordsController.js

Controlador para los registros emocionales del usuario. Gestiona listado, creación y resúmenes mensuales de emociones y carga cognitiva.

## Funciones exportadas

### `listByUser(req, res)`

Lista los registros emocionales de un usuario con filtros opcionales.

**Parámetros de ruta:** `userId`  
**Query params:** `date` (YYYY-MM-DD, opcional), `stateId` (número entero, opcional)

- Valida que `stateId`, cuando se provee, sea numérico; devuelve `400` si no lo es.
- Llama a `emotionalRecordsService.listEmotionalRecordsByUser(userId, date, stateId)`.
- Devuelve `200` con el array de registros.

**Ruta asociada:** `GET /emotionalrecords/:userId/list`

---

### `createForUser(req, res)`

Crea un nuevo registro emocional para el usuario autenticado.

**Parámetros de ruta:** `userId`  
**Cuerpo:** `{ emotional_state_id: number }`

- Verifica que el `sub` del token JWT (`req.auth.sub`) coincida con `userId`; devuelve `403` si no coincide.
- Valida que `emotional_state_id` sea un número; devuelve `400` si falta o es inválido.
- Llama a `emotionalRecordsService.createEmotionalRecord(userId, emotionalStateId)`.
- Devuelve `201` con el registro creado, incluido el nombre del estado emocional.

**Ruta asociada:** `POST /emotionalrecords/:userId/create`

---

### `getMonthlySummaryByUser(req, res)`

Resumen diario del mes: estados emocionales y número de tareas con vencimiento por día.

**Parámetros de ruta:** `userId`, `month` (nombre en español, ej. `enero`)  
**Query params:** `year` (YYYY)

- Valida que `year` tenga formato de 4 dígitos; devuelve `400` si no.
- Llama a `emotionalRecordsService.getMonthlySummaryByUser({ userId, month, year })`.
- Devuelve `200` con un array de objetos `{ date, emotional_states[], tasks_due_count }` por cada día del mes.

**Ruta asociada:** `GET /:month/:userId`

---

### `getMonthlyCognitiveLoadByUser(req, res)`

Carga cognitiva promedio del usuario para un mes específico.

**Parámetros de ruta:** `userId`  
**Query params:** `month` (nombre en español o número 1-12), `year` (YYYY)

- Valida presencia de `month` y formato de `year`; devuelve `400` si faltan.
- Llama a `emotionalRecordsService.getMonthlyCognitiveLoadByUser({ userId, month, year })`.
- Devuelve `200` con `{ month, average_cognitive_load, records_count }`.

**Ruta asociada:** `GET /cognitive-load/:userId`

## Códigos de respuesta comunes

| Código | Descripción                                             |
|--------|---------------------------------------------------------|
| `200`  | Operación exitosa.                                      |
| `201`  | Registro creado correctamente.                          |
| `400`  | Parámetro faltante o con formato inválido.              |
| `403`  | El usuario autenticado no coincide con el userId objetivo. |
| `500`  | Error interno del servidor.                             |

## Dependencias

- `../services/emotionalRecordsService`
