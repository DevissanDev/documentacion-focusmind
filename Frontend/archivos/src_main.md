# src/main.jsx

Proposito
- Punto de entrada de la aplicacion.
- Configurar AWS Amplify (Cognito) y React Router.

Responsabilidades
- Inicializar Amplify con `VITE_AWS_USER_POOL_ID` y `VITE_AWS_USER_POOL_CLIENT_ID`.
- Montar el root de React y envolver con `BrowserRouter`.

Flujo basico
1) Configurar Amplify.
2) Renderizar `App` dentro del Router.

Entradas/Salidas
- Entradas: variables de entorno de Cognito.
- Salidas: app React montada en el root.

Dependencias
- react
- react-dom
- aws-amplify
- react-router-dom
- ./App

Notas
- Si faltan variables de Cognito, el login no funcionara.

Ejemplo
```js
// createRoot(...).render(<BrowserRouter><App /></BrowserRouter>);
```
