---
name: todo-trello
description: "Revisa las prácticas y proyectos pendientes de 4Geeks y, si Trello está conectado, crea tarjetas sin duplicados en sus listas correspondientes."
---

# Revisar pendientes de 4Geeks y sincronizarlos con Trello

## Procedimiento

1. Consulta las tareas asignadas del usuario mediante `GET https://breathecode.herokuapp.com/v1/assignment/user/me/task`. Usa `TOKEN_4GEEKS` desde el entorno o `/root/.openclaw/.env` en la cabecera `Authorization: Token <valor>`; nunca imprimas, registres ni incluyas el token en mensajes, archivos o salida de depuración. Si falta el token o la API falla, detente y comunica el problema sin inferir el progreso.
2. Lee la respuesta completa, siguiendo `limit` y `offset` si hay paginación. Considera únicamente `task_type=EXERCISE` como práctica y `task_type=PROJECT` como proyecto; no conviertas tareas `LESSON` en tarjetas.
3. Selecciona solo tareas con `task_status=PENDING` y `opened_at` no vacío: la marca de apertura es evidencia explícita de que Elena ya llegó a esa tarea. No uses `revision_status` para decidir si una tarea está pendiente, no incluyas tareas completadas ni tareas sin abrir, porque pueden ser de módulos futuros. Si el API deja de devolver `opened_at` o no permite distinguir las tareas ya alcanzadas, pregunta antes de sincronizar.
4. Comprueba que hay una conexión/herramienta de Trello disponible antes de realizar cambios. Usa el tablero `4Geeks` y las listas `Prácticas` y `Proyectos`. Si Trello no está accesible, no afirmes que se buscaron o crearon tarjetas; informa que la consulta de 4Geeks sí se pudo hacer y que la sincronización está bloqueada por falta de conexión.
5. Busca en la lista correspondiente antes de crear cada tarjeta. Compara títulos normalizados (sin distinguir mayúsculas, espacios repetidos ni diferencias triviales de acentuación) para evitar duplicados. Si ya existe, omítela; no edites ni archives tarjetas existentes.
6. Crea una tarjeta por cada tarea pendiente que no tenga equivalente: `EXERCISE` en `Prácticas`, `PROJECT` en `Proyectos`. Si el tablero o una lista no existe, detente sin crear en un destino alternativo y comunica cuál falta.
7. Verifica en Trello cada creación mediante una nueva lectura de la lista. Si el resultado de una creación es incierto, vuelve a buscar la tarjeta antes de reintentar. Resume conteos de pendientes, tarjetas creadas y duplicados omitidos; distingue claramente resultados verificados de operaciones bloqueadas o inciertas.

## Límites

- La API se consulta solo en modo lectura; nunca actualices tareas, entregas ni progreso.
- No incluyas tareas completadas, lecciones ni tareas futuras fuera del tramo alcanzado.
- No expongas credenciales ni datos personales innecesarios en la respuesta.
- No declares completada la sincronización sin verificar las tarjetas en Trello.
