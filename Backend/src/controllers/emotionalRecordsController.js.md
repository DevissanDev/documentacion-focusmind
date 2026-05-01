# src/controllers/emotionalRecordsController.js

Proposito
- Exponer endpoints para registros emocionales.
- Delegar consultas a la capa de servicio.

Responsabilidades
- Leer `userId` desde params.
- Devolver lista de registros o error.

Flujo basico
1) Extraer `userId`.
2) Llamar `listEmotionalRecordsByUser`.
3) Responder con JSON o 500.

Entradas/Salidas
- Entradas: `req.params.userId`.
- Salidas: JSON con registros o error.

Dependencias
- ../services/emotionalRecordsService

Notas
- Maneja errores con `status 500`.

Ejemplo
```js
// GET /emotionalrecords/123/list
```
