# src/middlewares/cognitoAuth.js

Middleware de autenticación basado en JWT de AWS Cognito. Verifica el token Bearer de cada petición antes de permitir el acceso a rutas protegidas.

## Flujo de validación

1. Lee las variables de entorno requeridas (`COGNITO_REGION`, `COGNITO_USER_POOL_ID`, `COGNITO_CLIENT_ID`).
2. Extrae el token del encabezado `Authorization: Bearer <token>`.
3. Obtiene el JWKS público del User Pool de Cognito (`/.well-known/jwks.json`).
4. Verifica la firma del JWT con `jwtVerify` de la librería `jose`.
5. Valida que `token_use` coincida con el tipo esperado (`access` por defecto).
6. Valida que la audiencia del token coincida con `COGNITO_CLIENT_ID`.
7. Si `COGNITO_ENFORCE_USER_MATCH=true` (valor por defecto), verifica que `payload.sub` sea igual a `req.params.userId`.
8. Adjunta el payload decodificado en `req.auth` y llama a `next()`.

## Variables de entorno

| Variable                     | Requerida | Descripción                                                                 |
|------------------------------|-----------|-----------------------------------------------------------------------------|
| `COGNITO_REGION`             | Sí        | Región AWS del User Pool (ej. `us-east-1`).                                |
| `COGNITO_USER_POOL_ID`       | Sí        | ID del User Pool de Cognito.                                               |
| `COGNITO_CLIENT_ID`          | Sí        | ID del cliente de la aplicación registrado en Cognito.                     |
| `COGNITO_TOKEN_USE`          | No        | Tipo de token a validar: `access` (defecto) o `id`.                        |
| `COGNITO_ENFORCE_USER_MATCH` | No        | Si es `"true"` (defecto), el `sub` del token debe coincidir con `userId`. |

## Respuestas de error

| Código | Condición                                                    |
|--------|--------------------------------------------------------------|
| `401`  | Token ausente, vacío, firma inválida, `token_use` incorrecto o audiencia inválida. |
| `403`  | El `sub` del token no coincide con el `userId` de la URL.   |

## Exportaciones

| Nombre       | Tipo       | Descripción               |
|--------------|------------|---------------------------|
| `cognitoAuth`| `function` | Middleware Express async. |

## Dependencias

- `jose` (v5+)
