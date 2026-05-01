# Estructura del proyecto

Proposito
- Explicar la organizacion de carpetas y el rol de cada capa.
- Definir responsabilidades y flujo de datos.

Raiz del repo
- `package.json`: scripts, dependencias y versionado.
- `vite.config.js`: configuracion de Vite.
- `.env`: variables locales (no se suben a Vercel).
- `README.md`: resumen general y stack.

src/
- `main.jsx`: entrada de la app, inicializa React, Amplify y Router.
- `App.jsx`: layout principal, rutas y control de sesion.
- `pages/`: paginas de rutas, componen UI y coordinan la logica.
- `features/`: dominios funcionales con UI, hooks y servicios propios.
- `components/`: UI reutilizable sin logica de API.
- `services/`: servicios compartidos (ej: `apiClient`).
- `hooks/`: hooks reutilizables comunes.
- `assets/`: imagenes e iconos locales.

Flujo de datos recomendado
1) Page solicita datos via hook de feature.
2) Hook llama a service de feature.
3) Service usa `apiFetch` y maneja errores basicos.
4) UI consume `loading`, `error` y `data`.

Reglas de arquitectura
- UI no debe llamar API directo: usar `features/*/services` o `src/services`.
- Los hooks encapsulan estado, carga y errores.
- Las paginas solo componen y coordinan.

Convenciones
- Nombres de archivos: `camelCase` para helpers y `PascalCase` para componentes.
- Evitar logica de negocio dentro de componentes visuales.
- Preferir `services` por feature si la API es especifica.
