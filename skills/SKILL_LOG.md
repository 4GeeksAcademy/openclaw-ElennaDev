# Registro de skills

## Consulta académica de 4Geeks mediante API

- **Sugerencia:** crear una skill de consulta académica de 4Geeks en modo de solo lectura y con autenticación segura. Reutilizar `todo-trello` para consultar los pendientes y conectarla a esa consulta; no crear otra skill para Trello.
- **Información compartida:** la mayoría de los endpoints requieren un token obtenido mediante `POST /v1/auth/login`, enviado en la cabecera `Authorization` con el prefijo `Token`. Se pueden consultar el perfil y las academias asociadas, cohortes y estados académicos, tareas, certificados, actividad propia, contenido educativo (lecciones, ejercicios y proyectos), tecnologías y eventos. La referencia señala `https://breathecode.herokuapp.com` como base habitual, aunque puede variar. También indiqué que la referencia no especifica el formato exacto de las credenciales ni de la respuesta del login.
- **¿Tuve que pedirte algo?:** no pedí información adicional para responder. Dejé la implementación pendiente, tal como solicitaste.

## Skill de autenticación de 4Geeks

- **Prompt original utilizado:** «Skill 1 - Autenticar. Crea un skill llamada 4geeks-auth en "skills/4geeks_auth" dentro de un archivo SKILL.md para comprobar mi autenticación con la API de 4geeks. Utiliza GET /v1/admissions/user/me y la variables "TOKEN_4GEEKS" con la cabecera "Authorization: [valor oculto]" Implementa y prueba unicamente esta skill. No expongas credenciales».
- **Nombre de la skill:** `4geeks-auth` (archivo: `skills/4geeks_auth/SKILL.md`).
- **Objetivo:** comprobar la autenticación de Elena en la API, sin mostrar el token ni los datos personales de la respuesta.
- **Endpoint utilizado:** `GET https://breathecode.herokuapp.com/v1/admissions/user/me`, con `TOKEN_4GEEKS` en la cabecera `Authorization`.
- **Prueba realizada:** validación del archivo de la skill y petición GET de comprobación.
- **Resultado real obtenido:** la validación indicó que la skill es válida y la petición respondió **HTTP 200**.
- **Estado del funcionamiento:** comprobación superada en esa prueba; HTTP 200 confirmó la autenticación en ese momento.

## Skill de proyectos de 4Geeks

- **Prompt original utilizado:** «skill 2 - Crea una skill llamada misProyectos en skills/mis-proyectos/SKILL.md, para recuperar la lista de proyectos asignados a mi con su estado actual (pendiente, entregado, calificado). Utiliza GET /v1/registry/asset, recurre al "task_status" y utiliza la variable "TOKEN_GEEKS" con la cabecera "authorization: [Valor oculto]. Implementa y prueba unicamente esta skill. No expongas credenciales». Después aprobaste cambiar la consulta al endpoint de assignments y aclaraste que la variable correcta es `TOKEN_4GEEKS`.
- **Nombre de la skill:** `mis-proyectos` (archivo: `skills/mis-proyectos/SKILL.md`).
- **Objetivo:** recuperar tus proyectos asignados y presentar su estado, distinguiendo entre pendiente, entregado pendiente de revisión y aprobado/calificado.
- **Cambio de GET:** se sustituyó `/v1/registry/asset`, que sirve para listar recursos del catálogo, por `/v1/assignment/user/me/task?task_type=PROJECT`, que consulta tus tareas asignadas de tipo proyecto y sus estados.
- **Endpoint utilizado:** `GET https://breathecode.herokuapp.com/v1/assignment/user/me/task?task_type=PROJECT`, con `TOKEN_4GEEKS` en la cabecera `Authorization`.
- **Prueba realizada:** validación del archivo de la skill y consulta real de la API.
- **Resultado real obtenido:** la skill pasó la validación y la API respondió **HTTP 200**. Devolvió 22 proyectos: `task_status` fue `DONE` en 18 y `PENDING` en 4; `revision_status` fue `APPROVED` en 17 y `PENDING` en 5.
- **Estado del funcionamiento:** comprobación superada; la consulta funcionó con la variable configurada en `/root/.openclaw/.env`. No se guardaron nombres de proyectos ni credenciales en este resumen.

## Skill para sincronizar pendientes de 4Geeks con Trello

- **Prompt original utilizado:** «skill 3 - Vamos a poner en marcha la skill "todo-trello" que ya tenemos creada, incluye el GET /v1/assignment/user/me/task y utiliza la variable "TOKEN_4GEEKS" con la cabecera "authorization: [Valor oculto]. Implementa y prueba unicamente esta skill. No expongas credenciales».
- **Nombre de la skill:** `todo-trello` (archivo: `skills/todo-trello/SKILL.md`).
- **Objetivo:** identificar prácticas y proyectos pendientes que ya se hayan abierto y crear en Trello solo las tarjetas que falten, evitando duplicados.
- **Endpoint utilizado:** `GET https://breathecode.herokuapp.com/v1/assignment/user/me/task`, con `TOKEN_4GEEKS` en la cabecera `Authorization`.
- **Prueba realizada:** validación de la skill, consulta real de la API y lectura de las listas de Trello para comprobar el resultado.
- **Resultado real obtenido:** la API respondió **HTTP 200** y devolvió 121 tareas, de las cuales 22 estaban pendientes. Se seleccionaron 10 prácticas y 2 proyectos ya abiertos. La validación indicó que la skill es válida; la verificación final encontró 10 tarjetas en “Prácticas” y 2 en “Proyectos”.
- **Estado del funcionamiento:** sincronización de prueba completada y verificada. No se guardó ni expuso el token.

## Skill de progreso de 4Geeks en Zapier Tables

- **Prompt original utilizado:** «skill 4 - Crea una última skill llamada Progreso 4Geeks que estará dentro de skills/progreso-4geeks/[SKILL.md](http://skill.md/) para obtener una visión general de cuánto he avanzado en el curso. Utiliza GET /v1/assignment/user/me/task y utiliza la variable "TOKEN_GEEKS" con la cabecera "authorization: [Valor oculto]. Implementa y prueba únicamente esta skill. No expongas credenciales . He conectado en Zapier una app llamada Zapier Tables, ya he creado la tabla llamada "Progreso 4Geeks", allí será donde introduciras los datos obtenidos a través del GET. (**Table ID:** `01M7T0QP1R7WH5SBA5HA88Q9QMS`)».
- **Nombre de la skill:** `progreso-4geeks` (archivo: `skills/progreso-4geeks/SKILL.md`).
- **Objetivo:** consultar las tareas de 4Geeks, resumir el progreso y sincronizar sus estados con la tabla indicada.
- **Endpoint utilizado:** `GET https://breathecode.herokuapp.com/v1/assignment/user/me/task`, con `TOKEN_4GEEKS` en la cabecera `Authorization`.
- **Destino de la sincronización:** tabla «Progreso 4Geeks», ID `01M7T0QP1R7WH5SBA5HA88Q9MS`, con las columnas `Modulo_ID`, `Modulo`, `Estado`, `Porcentaje` y `Notas`.
- **Mapeo de estados:** `DONE` o `APPROVED` → `Completado` (100 %); `REJECTED` → `En curso` (50 %); `PENDING` y otros estados → `Pendiente` (0 %).
- **Prueba realizada:** validación de la skill, consulta de la API, sincronización y lectura posterior de los registros para verificar el resultado.
- **Resultado real obtenido:** 121 tareas sincronizadas; 102 completadas y 19 pendientes. La verificación confirmó 121 IDs únicos, sin registros faltantes, duplicados ni diferencias en los campos.
- **Estado del funcionamiento:** sincronización completada y verificada. No se incluyeron credenciales en este registro.
