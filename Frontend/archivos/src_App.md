# src/App.jsx

Proposito
- Layout principal del dashboard.
- Control de rutas y estado de sesion.

Responsabilidades
- Mostrar sidebar y contenido principal.
- Redirigir segun el estado de autenticacion.
- Escuchar eventos de auth con `Hub`.

Flujo basico
1) Validar sesion con `getCurrentUser`.
2) Escuchar eventos `signedIn` y `signedOut`.
3) Renderizar rutas y layout segun auth.

Entradas/Salidas
- Entradas: estado de autenticacion del usuario.
- Salidas: UI con rutas protegidas o login.

Dependencias
- react-router-dom
- aws-amplify

Notas
- Protege rutas privadas y redirige a login cuando no hay sesion.

Ejemplo
```js
// <App />
```
