# app.js

Proposito
- Configurar la aplicacion Express.
- Registrar middlewares y rutas principales.

Responsabilidades
- Inicializar `express()` y `cors()`.
- Montar rutas de salud, tareas y registros emocionales.

Flujo basico
1) Crear instancia de Express.
2) Aplicar middlewares globales.
3) Registrar rutas y exportar `app`.

Entradas/Salidas
- Entradas: solicitudes HTTP a `/` y `/api`.
- Salidas: respuestas JSON de controladores.

Dependencias
- express
- ./src/routes/healthRoutes

Notas
- La ruta raiz `/` usa `healthController.getHelloWorld`.

Ejemplo
```js
// const app = require("./app");
```
