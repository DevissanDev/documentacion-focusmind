# src/routes/emotionalRecordsRoutes.js

Proposito
- Definir rutas de registros emocionales.
- Enlazar middleware de auth y controlador.

Responsabilidades
- Registrar GET de listado por usuario.
- Aplicar `cognitoAuth`.

Flujo basico
1) Crear `router`.
2) Definir ruta GET con middleware.
3) Exportar router.

Entradas/Salidas
- Entradas: `:userId` en URL.
- Salidas: JSON del controlador.

Dependencias
- express
- ../middlewares/cognitoAuth

Notas
- Ruta: `/emotionalrecords/:userId/list`.

Ejemplo
```js
// app.use("/", emotionalRecordsRoutes)
```
