# Nuevo proceso por sector — Cuenca del Plata: orden del circuito desde ventas

- **Fecha:** 2026-10-27
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-27-nuevo-proceso-por-sector-cuenca-del-plata-parte-2.md](2026-10-27-nuevo-proceso-por-sector-cuenca-del-plata-parte-2.md)

## Objetivo
La usuaria editó el Word a mano y pidió ordenar el circuito desde ventas: Reservas (ventas) → Operaciones → Proveedores → (Tesorería) → Administración, sin tocar sus modificaciones.

## Estado final
Terminado. `Trabajo/Entregables/Nuevo proceso por sector - Cuenca del Plata (marca Softur).docx` (+ `.pdf`) reemplazado, 7 páginas: 01 Reservas · 02 Operaciones · 03 Proveedores · 04 Tesorería · 05 Administración · 06 Escalamiento.

## Decisiones y por qué
- El Word vigente es **el editado por la usuaria**: no se regenera desde el script (el script `contenido-globos.ps1` quedó desactualizado respecto de sus cambios). `[decisión]`
- Se movieron bloques completos de XML (de cada título al siguiente) y sólo se cambiaron los números de sección y el orden de filas de la tabla "El circuito". Control: los 480 textos del documento son los mismos antes y después (sin contar los números). `[decisión]`
- Tesorería quedó entre Proveedores y Administración (la usuaria no la nombró). La tabla de escalamiento y la fila "Inicio de la implementación" de la portada no se tocaron. `[decisión]`
- Cambios propios de la usuaria detectados (no se tocaron): vuelos reconfirmados 72 h antes (Operaciones) y 48 h (globo de Reservas), datos faltantes de la reserva completos 96 h antes de la prestación, Proveedores ya no incluye hoteles en el paso 1, "Busca el planning" en el paso 2, gastos de servicios "funciona igual el circuito" sin globos. `[decisión]`

## Archivos, tablas y objetos relevantes
- Scripts en el scratchpad: `outline.ps1` (lista la estructura del cuerpo), `reordenar.ps1` (mueve secciones y renumera), `empaquetar.ps1` (compara textos, empaqueta y exporta PDF). Respaldo de la versión de la usuaria: `respaldo-version-usuaria.docx`.
- Softur.Serenity: no se consultó.

## Cambios hechos
- Reordenado el documento y exportado el PDF.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Si se vuelve a generar desde el script, se pierden los cambios manuales de la usuaria. Para próximos cambios, editar sobre el .docx de Entregables. `[decisión]`

## Pendientes
No aplica.

## Cómo validar
1. PDF: portada con el circuito 01 Reservas … 06 Escalamiento; cada sector en su página en ese orden.

## Datos que pueden quedar viejos
No aplica.
