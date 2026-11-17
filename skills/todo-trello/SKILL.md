---
name: todo-trello
description: "Revisa las prácticas y proyectos pendientes del curso y crea tarjetas en Trello."
---

**Habilidad:**  
Revisar las prácticas y proyectos pendientes del curso y organizarlos como tarjetas en Trello.

**Descripción**  
Consulta el progreso del curso mediante la API, identifica las prácticas y los proyectos sin terminar hasta el punto alcanzado y crea una tarjeta para cada uno en la lista correspondiente.

**Cuándo Usar**  
Cuando Elena pida revisar los pendientes del curso o crear en Trello tarjetas para las prácticas y los proyectos sin terminar.

**Prerrequisitos**
- Tener acceso a la API del curso para consultar el progreso. La API aún está pendiente de proporcionar.
- Tener disponible la conexión de Zapier con Trello.
- Usar este destino en Trello:
  - **Tablero:** `4Geeks`
  - **Lista `Prácticas`:** módulos sin terminar clasificados como prácticas.
  - **Lista `Proyectos`:** módulos sin terminar clasificados como proyectos.

**Procedimiento**
1. Consultar el progreso del curso mediante la API y en modo de solo lectura.
2. Identificar las prácticas y los proyectos sin terminar hasta el punto alcanzado. No incluir elementos completados ni de módulos futuros.
3. Buscar en la lista correspondiente del tablero `4Geeks` si ya existe una tarjeta con el mismo nombre.
4. Crear una tarjeta por cada elemento pendiente que aún no tenga una tarjeta correspondiente:
   - Práctica pendiente → lista `Prácticas`.
   - Proyecto pendiente → lista `Proyectos`.
5. Comprobar el resultado y resumir qué tarjetas se crearon y cuáles se omitieron.

**Resultado Esperado**  
Una tarjeta en la lista correspondiente por cada práctica o proyecto pendiente, sin duplicados, junto con un resumen de la revisión.

**Casos Especiales**
- Si la API no está disponible, pedir el acceso necesario y no inferir el progreso.
- Si no se puede determinar con claridad si un elemento está pendiente o si es una práctica o un proyecto, pedir aclaración antes de crear una tarjeta.
- Si la tarjeta ya existe, no duplicarla.
- Si no se puede confirmar si una tarjeta se creó, buscarla antes de volver a intentarlo.
- No modificar el progreso del curso ni editar o archivar tarjetas existentes.
