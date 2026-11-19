---
name: mis-proyectos
description: Consulta los proyectos asignados a Elena en 4Geeks y devuelve sus estados actuales sin modificar entregas.
---

# Consultar mis proyectos asignados

Cuando Elena pida ver sus proyectos asignados o sus estados, consulta únicamente sus tareas de tipo proyecto en modo de solo lectura.

1. Obtén `TOKEN_4GEEKS` del entorno; si no está definida, lee únicamente esa clave de `/root/.openclaw/.env` sin imprimir el valor. Si no existe o está vacía, informa que debe configurarse en el entorno seguro y detente; nunca pidas que se comparta por chat.
2. Envía `GET https://breathecode.herokuapp.com/v1/assignment/user/me/task?task_type=PROJECT` con la cabecera `Authorization: Token <valor de TOKEN_4GEEKS>`. Obtén el token directamente del entorno o de la clave indicada, no lo incluyas en argumentos visibles, archivos, registros, salidas ni mensajes. No uses `/v1/registry/asset` para consultar asignaciones o estados.
3. Si la respuesta está paginada, sigue `limit` y `offset` hasta completar la lista de proyectos asignados; evita peticiones repetidas innecesarias. No añadas un filtro `task_status` por defecto, para incluir proyectos en todos sus estados; cuando Elena solicite un estado concreto, puedes añadir el filtro `task_status` admitido por la API.
4. Para cada proyecto, presenta su título y los campos de estado disponibles (`task_status`, `revision_status` y, si es útil, si existe `delivered_at` o `reviewed_at`). Resume el estado sin confundir los campos: `task_status=PENDING` se muestra como **Pendiente**; si `delivered_at` existe y `revision_status=PENDING`, se muestra como **Entregado, pendiente de revisión**; si `revision_status=APPROVED`, se muestra como **Calificado/aprobado**. `task_status=DONE` significa completada por la estudiante y no demuestra por sí solo que esté calificada. La referencia define `task_status=REJECTED` como rechazada y requiere correcciones; si aparece, indícalo claramente. Para otros valores de `revision_status` o combinaciones contradictorias, muestra los valores originales y no infieras una categoría. No supongas que aprobación implica una nota numérica.
5. Si la respuesta no contiene proyectos, indícalo claramente. Si la API devuelve un error, informa solo del código HTTP o del tipo general del error y no muestres el token ni datos ajenos a la solicitud. No actualices ni entregues tareas.
