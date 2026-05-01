# Archivos clave

Proposito
- Dar contexto de archivos importantes y sus funciones.
- Servir como referencia rapida para nuevos colaboradores.

Entrada y layout
- `src/main.jsx`
	- Inicializa React y monta el root.
	- Configura Amplify con Cognito (User Pool).
	- Envuelve la app con `BrowserRouter`.

- `src/App.jsx`
	- Define el layout del dashboard con sidebar.
	- Maneja rutas y redireccion segun estado de auth.
	- Escucha eventos de autenticacion via `Hub`.

Servicios comunes
- `src/services/apiClient.js`
	- Wrapper de `fetch`.
	- Adjunta `Authorization: Bearer <access_token>`.
	- Reintenta en 401 con `forceRefresh`.

Feature: registro emocional
- `src/pages/RegistroEmocionalPage.jsx`
	- Compone el header y el listado.
	- Usa `useRegistroEmocional` para cargar datos.

- `src/features/registroEmocional/services/registroEmocionalApi.js`
	- Encapsula llamadas a `/emotionalrecords/:userId/list`.
	- Valida el estado HTTP antes de devolver JSON.

- `src/features/registroEmocional/hooks/useRegistroEmocional.js`
	- Resuelve el `userId` via Amplify.
	- Controla `loading`, `error` y `records`.

- `src/features/registroEmocional/components/RegistroEmocionalList.jsx`
	- Renderiza la tabla con estilos personalizados.
	- Mapea el estado emocional a iconos locales.

Feature: tareas
- `src/pages/TaskPage.jsx`
	- Layout de tareas y encabezados de columnas.
	- Renderiza `TaskList` y el CTA principal.

- `src/features/task/services/taskApi.js`
	- Encapsula llamadas a `/tasks/:userId/list`.
	- Valida el estado HTTP antes de devolver JSON.

- `src/features/task/hooks/useTasks.js`
	- Resuelve el `userId` via Amplify.
	- Controla `loading`, `error` y `tasks`.

- `src/features/task/components/TaskList.jsx`
	- Renderiza filas de tareas con el diseño solicitado.
	- Normaliza campos comunes del API.

Notas de configuracion
- `VITE_API_URL` debe existir en el entorno de deploy (Vercel).
- La ausencia de `VITE_API_URL` genera URLs `undefined/...`.
