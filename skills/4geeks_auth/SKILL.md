---
name: 4geeks-auth
description: Comprueba la autenticación de Elena en la API de 4Geeks consultando su perfil actual, sin mostrar ni guardar el token ni la respuesta personal.
---

# Comprobar autenticación de 4Geeks

Cuando Elena pida comprobar el acceso a la API de 4Geeks, realiza únicamente esta comprobación de solo lectura:

1. Comprueba que la variable de entorno `TOKEN_4GEEKS` está definida y no vacía. Si falta, informa que debe configurarse en el entorno seguro y detente; nunca pidas que pegue el token en el chat.
2. Envía una petición `GET` a `https://breathecode.herokuapp.com/v1/admissions/user/me` con la cabecera `Authorization: Token <valor de TOKEN_4GEEKS>`. Obtén el valor directamente del entorno; no lo incluyas en argumentos visibles, archivos, registros, salidas ni mensajes. No sustituyas el prefijo literal `Token ` requerido por la API.
3. Descarta el cuerpo de la respuesta para no revelar datos del perfil. Informa solo el resultado de autenticación y, si falla, el código HTTP; no imprimas el token ni detalles personales.
4. Interpreta `200` como autenticación aceptada. Interpreta `401` o `403` como acceso rechazado/no autorizado. Para otros códigos o errores de red, indica que la comprobación no pudo confirmar la autenticación. No reintentes con otros endpoints ni cambies datos.
