# src/features/registroEmocional/components/RegistroEmocionalList.jsx

Proposito
- UI del listado de registro emocional.

Responsabilidades
- Renderizar estados de carga, error y vacio.
- Mostrar filas con fecha, nombre e icono.
- Mapear `name` o `emotional_state_id` a iconos.

Flujo basico
1) Mostrar loader o mensaje de error.
2) Renderizar estado vacio si no hay datos.
3) Renderizar filas con iconos.

Entradas/Salidas
- Entradas: props con `records`, `loading`, `error`.
- Salidas: tabla/listado renderizado.

Dependencias
- React
- assets locales (iconos)

Notas
- Normaliza el estado emocional para mapear iconos.

Ejemplo
```js
// <RegistroEmocionalList records={records} loading={loading} error={error} />
```
