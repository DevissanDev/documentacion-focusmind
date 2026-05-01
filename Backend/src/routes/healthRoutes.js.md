# src/routes/healthRoutes.js

Proposito
- Definir endpoints de salud.
- Exponer verificacion de servicio y DB.

Responsabilidades
- Registrar rutas `/hola-mundo` y `/health`.
- Delegar en `healthController`.

Flujo basico
1) Crear `router`.
2) Definir rutas GET.
3) Exportar router.

Entradas/Salidas
- Entradas: solicitudes HTTP sin params.
- Salidas: JSON de salud.

Dependencias
- express
- ../controllers/healthController

Notas
- Se monta bajo prefijo `/api` en app.js.

Ejemplo
```js
// GET /api/health
```
