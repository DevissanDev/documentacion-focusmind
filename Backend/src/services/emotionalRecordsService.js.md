# src/services/emotionalRecordsService.js

Proposito
- Consultar registros emocionales en Postgres.
- Entregar datos listos para el controlador.

Responsabilidades
- Ejecutar query con join a `emotional_states`.
- Ordenar por fecha descendente.

Flujo basico
1) Construir SQL parametrizado.
2) Ejecutar `pool.query`.
3) Retornar `rows`.

Entradas/Salidas
- Entradas: `userId`.
- Salidas: array de registros.

Dependencias
- ./postgresClient

Notas
- Usa parametro `$1` para evitar SQL injection.

Ejemplo
```js
// const rows = await listEmotionalRecordsByUser("123");
```
