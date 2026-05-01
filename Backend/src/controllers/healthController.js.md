# src/controllers/healthController.js

Proposito
- Proveer endpoints de salud y verificacion DB.
- Centralizar respuestas de estado.

Responsabilidades
- Ejecutar `testConnection` para validar DB.
- Armar respuesta de salud con `healthService`.

Flujo basico
1) Ejecutar prueba de conexion.
2) Preparar respuesta segun resultado.
3) Responder con JSON.

Entradas/Salidas
- Entradas: sin parametros de negocio.
- Salidas: JSON con estado o error.

Dependencias
- ../services/healthService
- ../services/postgresClient

Notas
- `getHelloWorld` depende de conexion a Postgres.

Ejemplo
```js
// GET /health
```
