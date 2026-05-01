# src/pages/RegistroEmocionalPage.jsx

Proposito
- Pagina del registro emocional.

Responsabilidades
- Renderizar encabezado y listado.
- Consumir el hook `useRegistroEmocional`.

Flujo basico
1) Ejecutar `useRegistroEmocional` al montar.
2) Mostrar encabezado con titulo.
3) Renderizar el listado con scroll interno.

Entradas/Salidas
- Entradas: estado del hook `useRegistroEmocional`.
- Salidas: UI del registro emocional.

Dependencias
- ../features/registroEmocional/hooks/useRegistroEmocional
- ../features/registroEmocional/components/RegistroEmocionalList

Notas
- Encabezado con titulo y emojis.

Ejemplo
```js
// <RegistroEmocionalPage />
```
