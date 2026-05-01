# src/services/healthService.js

Proposito
- Construir respuesta de salud del sistema.
- Integrar estado de base de datos.

Responsabilidades
- Generar timestamp y estado general.
- Marcar estado DB segun `testConnection`.

Flujo basico
1) Inicializar objeto base.
2) Ejecutar `testConnection`.
3) Ajustar `database` y devolver.

Entradas/Salidas
- Entradas: sin parametros.
- Salidas: objeto de estado.

Dependencias
- ./postgresClient

Notas
- Incluye `databaseError` si falla la conexion.

Ejemplo
```js
// const status = await getHealthStatus();
```
