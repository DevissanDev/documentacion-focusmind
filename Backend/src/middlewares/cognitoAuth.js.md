# src/middlewares/cognitoAuth.js

Proposito
- Validar tokens JWT de Cognito.
- Proteger rutas por usuario y audiencia.

Responsabilidades
- Leer variables de entorno requeridas.
- Verificar token, issuer y audiencia.

Flujo basico
1) Obtener config de Cognito desde env.
2) Validar header Authorization y JWT.
3) Adjuntar `req.auth` o responder 401/403.

Entradas/Salidas
- Entradas: `Authorization: Bearer <token>`, `req.params.userId`.
- Salidas: `next()` o respuesta de error JSON.

Dependencias
- jose
- process.env

Notas
- Requiere `COGNITO_*` definidos para funcionar.

Ejemplo
```js
// router.get("/tasks/:userId/list", cognitoAuth, handler)
```
