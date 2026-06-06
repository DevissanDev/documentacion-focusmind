# src/routes/emotionalRecordsRoutes.js

Router para los registros emocionales y carga cognitiva. Todas las rutas requieren autenticación Cognito.

## Rutas

| Método  | Ruta                             | Auth    | Controlador                                              | Descripción                              |
|---------|----------------------------------|---------|----------------------------------------------------------|------------------------------------------|
| `GET`   | `/emotionalrecords/:userId/list` | Cognito | `emotionalRecordsController.listByUser`                  | Lista los registros emocionales del usuario. |
| `POST`  | `/emotionalrecords/:userId/create` | Cognito | `emotionalRecordsController.createForUser`             | Crea un nuevo registro emocional.        |
| `GET`   | `/cognitive-load/:userId`        | Cognito | `emotionalRecordsController.getMonthlyCognitiveLoadByUser` | Carga cognitiva promedio mensual.       |
| `GET`   | `/:month/:userId`                | Cognito | `emotionalRecordsController.getMonthlySummaryByUser`     | Resumen diario del mes (emociones + tareas). |

## Middleware de validación de mes

Antes de la ruta `/:month/:userId` se aplica `ensureValidMonth`, que verifica que el parámetro `:month` sea un nombre de mes válido en español:

```
enero, febrero, marzo, abril, mayo, junio,
julio, agosto, septiembre, setiembre, octubre, noviembre, diciembre
```

Si el mes no es válido, el middleware llama a `next("route")` para saltar la ruta (no devuelve error directamente).

## Montaje en app.js

Este router se monta **dos veces**:
- Bajo `/api` → rutas con prefijo `/api/emotionalrecords/...`
- Bajo `/` → rutas sin prefijo `/emotionalrecords/...`

## Dependencias

- `express`
- `../controllers/emotionalRecordsController`
- `../middlewares/cognitoAuth`
