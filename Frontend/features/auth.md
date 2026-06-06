# Feature: Autenticación

Gestiona el flujo completo de autenticación del usuario mediante AWS Cognito. Incluye login, registro, verificación OTP, configuración de MFA (TOTP), recuperación de contraseña y "remember device".

## Archivos relevantes

```
src/components/Auth/
├── Login.jsx                  # Orquestador principal del flujo de login
├── Register.jsx               # Registro de nuevos usuarios
├── CodeInputGroup.jsx         # Input de código de 6 dígitos
├── constants/
│   ├── authState.js           # Enum de estados del flujo de auth
│   └── authText.js            # Textos/labels de la UI
├── utils/
│   └── authErrorMapper.js     # Mapeo de errores Cognito → mensajes amigables
└── ui/
    ├── AuthPanel.jsx          # Contenedor visual del formulario
    ├── AuthTextField.jsx      # Campo de texto estilizado
    ├── AuthCheckboxField.jsx  # Checkbox estilizado
    ├── AuthDivider.jsx        # Separador visual
    └── AuthErrorMessage.jsx   # Bloque de mensaje de error
```

```
src/hooks/
└── useLoginFlow.js            # Lógica del flujo de login (estados + callbacks)
```

## Estados del flujo de login

El componente `Login` opera como una máquina de estados. Cada estado renderiza un sub-formulario distinto.

| Estado | Descripción |
|--------|-------------|
| `EMAIL_INPUT` | Pantalla inicial — ingreso de correo |
| `OTP_INPUT` | Verificación con código OTP enviado por email |
| `PASSWORD_INPUT` | Login con contraseña |
| `TOTP_INPUT` | Verificación TOTP (autenticador) |
| `FORGOT_PASSWORD` | Solicitar código de recuperación |
| `RESET_PASSWORD` | Ingresar código + nueva contraseña |
| `MFA_SETUP` | Configurar TOTP por primera vez (muestra QR) |

## Flujos de autenticación

### Flujo OTP (passwordless)

```
EMAIL_INPUT → (envía OTP) → OTP_INPUT → (confirma OTP) → autenticado
```

### Flujo contraseña

```
EMAIL_INPUT → (usuario tiene contraseña) → PASSWORD_INPUT → autenticado
```

### Flujo con MFA activo

```
PASSWORD_INPUT → (Cognito pide TOTP) → TOTP_INPUT → autenticado
```

### Flujo recuperación de contraseña

```
PASSWORD_INPUT → (olvidé contraseña) → FORGOT_PASSWORD → RESET_PASSWORD → EMAIL_INPUT
```

### Flujo configuración inicial de MFA

```
autenticado → (Cognito requiere setup TOTP) → MFA_SETUP → autenticado
```

## Hook: `useLoginFlow`

Centraliza toda la lógica de mutación de estado y llamadas a AWS Amplify.

```js
const {
  state,          // Estado actual del flujo
  loading,        // Indicador de carga
  error,          // Mensaje de error activo
  handlers,       // { handleEmailSubmit, handleOtpSubmit, handlePasswordSubmit, ... }
} = useLoginFlow({ onLoginSuccess })
```

## Dependencias AWS Amplify utilizadas

| Función | Uso |
|---------|-----|
| `signIn` | Inicio de sesión con email/contraseña |
| `signUp` | Registro de nuevo usuario |
| `confirmSignUp` | Confirmar registro con código OTP |
| `confirmSignIn` | Confirmar OTP/TOTP en flujos challenge |
| `resetPassword` | Solicitar código de recuperación |
| `confirmResetPassword` | Confirmar nuevo password con código |
| `setUpTOTP` | Obtener URI para configurar autenticador |
| `verifyTOTPSetup` | Verificar configuración TOTP |
| `updateMFAPreference` | Activar/desactivar MFA |
| `rememberDevice` | Recordar dispositivo actual |
| `getCurrentUser` | Obtener usuario de sesión activa |
| `signOut` | Cerrar sesión |
| `Hub.listen('auth', ...)` | Escuchar eventos de autenticación |

## Manejo de errores

`authErrorMapper.js` traduce los códigos de error de Cognito a mensajes en español:

| Código Cognito | Mensaje mostrado |
|----------------|-----------------|
| `NotAuthorizedException` | Contraseña incorrecta |
| `UserNotFoundException` | Usuario no encontrado |
| `CodeMismatchException` | Código incorrecto |
| `ExpiredCodeException` | Código expirado |
| `UsernameExistsException` | El correo ya está registrado |
| `LimitExceededException` | Demasiados intentos, espera un momento |

## Props de `Login`

| Prop | Tipo | Descripción |
|------|------|-------------|
| `onLoginSuccess` | `() => void` | Callback al autenticar correctamente |
| `onNavigate` | `() => void` | Callback para navegar a `/register` |

## Props de `Register`

| Prop | Tipo | Descripción |
|------|------|-------------|
| `onNavigate` | `() => void` | Callback para volver a `/login` |
