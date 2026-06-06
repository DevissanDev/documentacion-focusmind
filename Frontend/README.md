# FocusMind — Documentación del Proyecto

FocusMind es una aplicación web de bienestar y productividad que integra gestión de tareas, registro emocional, calendario visual y analíticas cognitivas, con autenticación segura mediante AWS Cognito.

## Stack tecnológico

| Categoría | Tecnología |
|-----------|-----------|
| Framework | React 19 + Vite 7 |
| Enrutamiento | React Router DOM 7 |
| Autenticación | AWS Amplify 6 + Cognito |
| Estilos | Tailwind CSS 4 |
| UI Libraries | PrimeReact 10, Material-UI 9 |
| Gráficos | @mui/x-charts 9 |
| Íconos | lucide-react, primeicons |
| HTTP | Fetch API (wrapper propio) |
| Deploy | Vercel (SPA routing) |

## Estructura de carpetas

```
src/
├── components/        # Componentes globales (Auth, Profile)
├── features/          # Módulos por dominio (calendar, task, etc.)
│   ├── calendar/
│   ├── dashboard/
│   ├── registroEmocional/
│   └── task/
├── pages/             # Páginas que ensamblan features
├── services/          # Cliente HTTP centralizado
├── hooks/             # Hooks globales
└── utils/             # Utilidades
```

## Rutas de la aplicación

| Ruta | Página | Auth requerida |
|------|--------|----------------|
| `/login` | Login | No |
| `/register` | Registro | No |
| `/dashboard` | Dashboard | Sí |
| `/tareas` | Gestión de tareas | Sí |
| `/registro-emocional` | Registro emocional | Sí |
| `/calendario` | Calendario | Sí |
| `/user` | Seguridad y perfil | Sí |

## Variables de entorno

```env
VITE_API_URL=http://localhost:3000
VITE_AWS_REGION=us-east-1
VITE_AWS_USER_POOL_ID=us-east-1_xxxxxxxxx
VITE_AWS_USER_POOL_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxx
```

## Scripts

```bash
npm run dev       # Servidor de desarrollo
npm run build     # Build de producción
npm run preview   # Preview del build
npm run lint      # Linting con ESLint
```

## Índice de documentación

### Features
- [Autenticación](features/auth.md)
- [Dashboard](features/dashboard.md)
- [Tareas](features/task.md)
- [Registro Emocional](features/registro-emocional.md)
- [Calendario](features/calendar.md)

### Componentes
- [Componentes de Autenticación](components/auth-components.md)
- [Componentes de Perfil](components/profile-components.md)
- [Componentes de Calendario](components/calendar-components.md)
- [Componentes de Tareas](components/task-components.md)

### Servicios
- [API Client](components/api-client.md)
