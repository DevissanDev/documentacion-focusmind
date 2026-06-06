# Componentes: Perfil y Seguridad

Componentes que conforman la página de seguridad de la cuenta (`/user`). Todos viven en `src/components/Profile/`.

---

## `Profile` (raíz)

**Archivo**: [src/components/Profile/Profile.jsx](../../src/components/Profile/Profile.jsx)

Componente orquestador de la página de seguridad. Ensambla todas las tarjetas de configuración y gestiona el estado compartido (loading, feedback, MFA status, etc.).

```jsx
<Profile onBack={() => navigate('/dashboard')} />
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `onBack` | `() => void` | Callback para volver al dashboard |

Usa el hook `useProfileSecurity` para toda la lógica.

---

## `ProfileHeader`

**Archivo**: [src/components/Profile/ui/ProfileHeader.jsx](../../src/components/Profile/ui/ProfileHeader.jsx)

Encabezado de la página con el nombre/email del usuario, avatar generado y botón de regreso.

```jsx
<ProfileHeader user={user} onBack={onBack} />
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `user` | `CognitoUser` | Objeto de usuario autenticado |
| `onBack` | `() => void` | Callback del botón "Volver" |

---

## `MfaStatusCard`

**Archivo**: [src/components/Profile/ui/MfaStatusCard.jsx](../../src/components/Profile/ui/MfaStatusCard.jsx)

Tarjeta que muestra el estado actual del MFA (TOTP) y permite activarlo o desactivarlo.

Cuando se activa por primera vez, muestra el código QR generado por `setUpTOTP` de AWS Amplify para escanear con un autenticador (Google Authenticator, Authy, etc.).

```jsx
<MfaStatusCard
  isMfaEnabled={true}
  onToggle={handleToggleMfa}
  qrUri={qrUri}
  loading={loading}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `isMfaEnabled` | `boolean` | Estado actual del MFA |
| `onToggle` | `() => void` | Callback para activar/desactivar |
| `qrUri` | `string?` | URI del QR para setup de TOTP |
| `loading` | `boolean` | Estado de carga de la operación |

Usa `qrcode.react` para renderizar el código QR.

---

## `DevicesCard`

**Archivo**: [src/components/Profile/ui/DevicesCard.jsx](../../src/components/Profile/ui/DevicesCard.jsx)

Tarjeta que lista los dispositivos de confianza ("remembered devices") de la cuenta y permite olvidarlos individualmente.

```jsx
<DevicesCard
  devices={devices}
  onForgetDevice={handleForgetDevice}
  loading={loading}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `devices` | `Device[]` | Lista de dispositivos recordados |
| `onForgetDevice` | `(deviceKey: string) => void` | Callback para olvidar un dispositivo |
| `loading` | `boolean` | Estado de carga |

---

## `DangerZoneCard`

**Archivo**: [src/components/Profile/ui/DangerZoneCard.jsx](../../src/components/Profile/ui/DangerZoneCard.jsx)

Tarjeta de acciones destructivas/irreversibles:
- **Cerrar sesión en todos los dispositivos**: invalida todas las sesiones activas via Cognito

```jsx
<DangerZoneCard
  onGlobalSignOut={handleGlobalSignOut}
  loading={loading}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `onGlobalSignOut` | `() => void` | Callback para cerrar sesión global |
| `loading` | `boolean` | Estado de carga de la operación |

Incluye confirmación visual antes de ejecutar la acción.

---

## `ProfileFeedback`

**Archivo**: [src/components/Profile/ui/ProfileFeedback.jsx](../../src/components/Profile/ui/ProfileFeedback.jsx)

Componente de notificación/toast que muestra el resultado de las operaciones de seguridad (éxito o error).

```jsx
<ProfileFeedback
  message="MFA activado correctamente"
  type="success"
  onDismiss={() => setFeedback(null)}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `message` | `string` | Texto del mensaje |
| `type` | `"success" \| "error"` | Tipo de alerta |
| `onDismiss` | `() => void` | Callback para cerrar |

---

## Hook: `useProfileSecurity`

**Archivo**: [src/hooks/useProfileSecurity.js](../../src/hooks/useProfileSecurity.js)

Centraliza toda la lógica de seguridad de la cuenta.

```js
const {
  user,              // CognitoUser
  devices,           // Device[]
  isMfaEnabled,      // boolean
  loading,           // boolean
  feedback,          // { message, type } | null
  qrUri,             // string | null
  handleToggleMfa,   // () => Promise<void>
  handleForgetDevice,// (deviceKey) => Promise<void>
  handleGlobalSignOut,// () => Promise<void>
} = useProfileSecurity()
```
