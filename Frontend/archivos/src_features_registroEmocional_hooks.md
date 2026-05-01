# src/features/registroEmocional/hooks/useRegistroEmocional.js

Proposito
- Hook de carga para registros emocionales.

Responsabilidades
- Resolver `userId` con Amplify.
- Gestionar `records`, `loading` y `error`.
- Invocar `registroEmocionalApi`.

Flujo basico
1) Obtener `userId` de la sesion.
2) Llamar a `registroEmocionalApi`.
3) Actualizar estado local.

Entradas/Salidas
- Entradas: sesion de usuario.
- Salidas: `{ records, loading, error }`.

Dependencias
- ../../services/registroEmocionalApi
- aws-amplify

Notas
- Maneja estado de carga y error para UI.

Ejemplo
```js
// const { records, loading, error } = useRegistroEmocional();
```
