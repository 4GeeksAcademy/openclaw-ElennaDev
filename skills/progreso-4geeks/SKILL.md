---
name: progreso-4geeks
description: "Cuando Ele pida un resumen de su avance en 4Geeks, consulta sus tareas asignadas, calcula el progreso y sincroniza los registros en Zapier Tables."
---

# Consultar y resumir el progreso de 4Geeks

1. Comprueba que `TOKEN_4GEEKS` esté disponible de forma segura. Si falta, detente sin pedir que se comparta por chat. No sustituyas otra variable de token sin autorización.
2. Consulta `GET https://breathecode.herokuapp.com/v1/assignment/user/me/task` con `Authorization: Token <TOKEN_4GEEKS>`. Sigue `limit` y `offset` hasta leer todas las tareas; no modifiques tareas ni entregas.
3. Resume el avance usando los `task_status` recibidos: cuenta como completadas las tareas `DONE` o `APPROVED`; informa por separado las `PENDING`, `REJECTED` y cualquier estado desconocido. Calcula el porcentaje completado sobre el total de tareas asignadas y explica el numerador y denominador. Separa los conteos por `task_type` si la respuesta lo permite; no infieras progreso a partir de `revision_status`.

## Configuración y esquema exacto de Zapier Tables

4. Antes de escribir, verifica que las herramientas MCP de **Zapier Tables** estén conectadas y apunta exclusivamente a esta tabla:
   - **Nombre de la tabla:** `Progreso 4Geeks`
   - **Table ID:** `01M7T0QP1R7WH5SBA5HA88Q9MS`
   - **Panel visual asociado:** `Seguimiento de módulos`
   - **Columnas existentes y tipos:**
     - `Modulo_ID` (Text): Clave única e invariable para evitar duplicados (usa el `id` o `associated_slug` de la tarea/módulo en 4Geeks).
     - `Modulo` (Text): Título o nombre legible de la tarea/módulo (`title` o `associated_slug`).
     - `Estado` (Dropdown — **solo acepta estos 3 valores literales**): `Pendiente`, `En curso`, `Completado`.
     - `Porcentaje` (Number): Valor numérico entero de `0` a `100`.
     - `Notas` (Text): Detalles adicionales (`task_type`, `task_status` original, enlace de `github_url` si existe o motivo de rechazo).
   - No inventes ni envíes campos fuera de estas 5 columnas, ni modifiques la estructura de la tabla.

## Reglas de mapeo y sincronización

5. Sincroniza un registro por tarea/elemento usando `Modulo_ID` como identificador estable:
   - Ejecuta primero `Find Records` filtrando por `Modulo_ID` sobre la tabla `01M7T0QP1R7WH5SBA5HA88Q9MS`.
   - Si el registro ya existe, usa `Update Record` con su `Record ID` interno; si no existe, usa `Create Record` (o `Create Multiple Records` en la carga inicial). No dupliques registros al repetir la consulta.
   - **Mapeo obligatorio hacia el Dropdown `Estado` y `Porcentaje`:**
     - `DONE` o `APPROVED` → `Estado`: `Completado` | `Porcentaje`: `100`
     - `REJECTED` → `Estado`: `En curso` | `Porcentaje`: `50` (indica en `Notas` que el estado en 4Geeks es `REJECTED`)
     - `PENDING` o cualquier otro estado → `Estado`: `Pendiente` | `Porcentaje`: `0`
6. Lee de nuevo los registros modificados para comprobar la sincronización. Informa el resumen completo y el resultado de la verificación sin revelar credenciales ni datos personales innecesarios, recordando que el panel `Seguimiento de módulos` en Zapier ya muestra los datos actualizados.
