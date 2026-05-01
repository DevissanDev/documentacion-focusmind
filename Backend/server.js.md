# server.js

Proposito
- Cargar variables de entorno.
- Levantar el servidor HTTP.

Responsabilidades
- Importar `app` y escuchar en `PORT`.
- Informar en consola el puerto activo.

Flujo basico
1) Cargar `.env`.
2) Resolver `PORT`.
3) Ejecutar `app.listen`.

Entradas/Salidas
- Entradas: `process.env.PORT`.
- Salidas: servidor escuchando en un puerto.

Dependencias
- dotenv
- ./app

Notas
- Si `PORT` no existe, usa 3000.

Ejemplo
```js
// node server.js
```
