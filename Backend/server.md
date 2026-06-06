# server.js

Punto de arranque del proceso Node. Carga las variables de entorno y pone a escuchar el servidor HTTP.

## Comportamiento

1. Ejecuta `require("dotenv").config()` para inyectar las variables del archivo `.env` en `process.env`.
2. Importa la aplicación Express desde `app.js`.
3. Escucha en el puerto indicado por `process.env.PORT` o en el puerto `3000` por defecto.
4. Imprime en consola `Server listening on port <PORT>` cuando el servidor arranca con éxito.

## Variables de entorno relevantes

| Variable | Tipo    | Descripción                                    |
|----------|---------|------------------------------------------------|
| `PORT`   | número  | Puerto HTTP en el que escucha el servidor. Valor por defecto: `3000`. |

## Dependencias

- `dotenv`
- `./app`
