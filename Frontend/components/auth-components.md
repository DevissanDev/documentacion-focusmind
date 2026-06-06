# Componentes: Autenticación

Componentes de UI que conforman la pantalla de login y registro. Todos viven en `src/components/Auth/`.

---

## `AuthPanel`

**Archivo**: [src/components/Auth/ui/AuthPanel.jsx](../../src/components/Auth/ui/AuthPanel.jsx)

Contenedor visual principal de cualquier formulario de autenticación. Aplica la tarjeta blanca centrada con sombra sobre el fondo oscuro.

```jsx
<AuthPanel title="Iniciar sesión" subtitle="Bienvenido de nuevo">
  {/* contenido del formulario */}
</AuthPanel>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `title` | `string` | Título principal del panel |
| `subtitle` | `string` | Subtítulo descriptivo |
| `children` | `ReactNode` | Contenido del formulario |

---

## `AuthTextField`

**Archivo**: [src/components/Auth/ui/AuthTextField.jsx](../../src/components/Auth/ui/AuthTextField.jsx)

Campo de texto estilizado para formularios de auth. Incluye label, input y estado de error.

```jsx
<AuthTextField
  label="Correo electrónico"
  type="email"
  value={email}
  onChange={(e) => setEmail(e.target.value)}
  error="El correo no es válido"
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `label` | `string` | Etiqueta visible del campo |
| `type` | `string` | Tipo de input (`email`, `password`, `text`) |
| `value` | `string` | Valor controlado |
| `onChange` | `function` | Handler de cambio |
| `error` | `string?` | Mensaje de error (opcional) |
| `disabled` | `boolean?` | Deshabilita el campo |

---

## `AuthCheckboxField`

**Archivo**: [src/components/Auth/ui/AuthCheckboxField.jsx](../../src/components/Auth/ui/AuthCheckboxField.jsx)

Checkbox estilizado para opciones como "Recordar este dispositivo" o "Acepto los términos".

```jsx
<AuthCheckboxField
  label="Recordar este dispositivo"
  checked={remember}
  onChange={(checked) => setRemember(checked)}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `label` | `string` | Texto descriptivo del checkbox |
| `checked` | `boolean` | Estado controlado |
| `onChange` | `(checked: boolean) => void` | Handler de cambio |

---

## `AuthErrorMessage`

**Archivo**: [src/components/Auth/ui/AuthErrorMessage.jsx](../../src/components/Auth/ui/AuthErrorMessage.jsx)

Bloque de error con ícono y texto en rojo. Aparece debajo del formulario cuando hay un error global (no de campo).

```jsx
<AuthErrorMessage message="Contraseña incorrecta. Inténtalo de nuevo." />
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `message` | `string` | Texto del error a mostrar |

Renderiza `null` si `message` está vacío o es `undefined`.

---

## `AuthDivider`

**Archivo**: [src/components/Auth/ui/AuthDivider.jsx](../../src/components/Auth/ui/AuthDivider.jsx)

Separador visual horizontal con texto central (ej: "o continúa con").

```jsx
<AuthDivider text="o" />
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `text` | `string?` | Texto central (default: `"o"`) |

---

## `CodeInputGroup`

**Archivo**: [src/components/Auth/CodeInputGroup.jsx](../../src/components/Auth/CodeInputGroup.jsx)

Input especializado para ingresar códigos de 6 dígitos (OTP / TOTP). Renderiza 6 celdas individuales con auto-avance y soporte de pegar.

```jsx
<CodeInputGroup
  value={code}
  onChange={setCode}
  disabled={loading}
/>
```

| Prop | Tipo | Descripción |
|------|------|-------------|
| `value` | `string` | Código de 6 dígitos como string |
| `onChange` | `(value: string) => void` | Callback con el código completo |
| `disabled` | `boolean?` | Deshabilita todas las celdas |

**Comportamiento**:
- Auto-avance al siguiente campo al escribir un dígito
- Retrocede al campo anterior al borrar
- Soporta pegar el código completo (Ctrl+V)
- Solo acepta caracteres numéricos
