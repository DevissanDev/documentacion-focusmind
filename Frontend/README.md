# Documentacion del proyecto

Proposito
- Documentar el frontend med-web de forma clara y operativa.
- Explicar la estructura, el flujo de datos y las reglas de arquitectura.

Resumen ejecutivo
- Stack: React + Vite + Tailwind + AWS Amplify (Cognito).
- Navegacion: React Router.
- API: llamadas via `fetch` con token `access_token`.
- Deploy: variables de entorno definidas en el proveedor (Vercel).

Instalacion y uso
1) Instalar dependencias: `npm install`
2) Desarrollo local: `npm run dev`


Variables de entorno
- `VITE_API_URL`: base URL del backend. Ej: https://med-core.onrender.com
- `VITE_AWS_USER_POOL_ID`: Cognito User Pool ID.
- `VITE_AWS_USER_POOL_CLIENT_ID`: Cognito App Client ID.

Nota de deploy
- En Vercel, configurar las mismas variables en Project Settings.
- Si falta `VITE_API_URL`, el frontend genera URLs `undefined/...`.

Estructura (alto nivel)
- `src/`: codigo fuente.
- `src/pages/`: paginas (rutas).
- `src/features/`: features con UI, hooks y servicios.
- `src/services/`: servicios comunes (api, helpers).
- `src/components/`: UI compartida.
- `src/hooks/`: hooks reutilizables.
- `src/assets/`: imagenes e iconos locales.

Guia rapida de arquitectura
- Las paginas orquestan el flujo y componen componentes.
- Los hooks encapsulan estado, carga y errores.
- La logica de API vive en `services`.

Indice de documentos
- Ver estructura y responsabilidades en `estructura.md`.
- Ver descripcion detallada de archivos en `archivos-clave.md`.
