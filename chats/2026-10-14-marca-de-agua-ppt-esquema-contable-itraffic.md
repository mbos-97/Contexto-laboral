# Marca de agua y versión no editable del PPT "Esquema administrativo-contable iTRAFFIC"

- **Fecha:** 2026-10-14
- **Proyecto / cliente:** Presentación para compartir con un cliente (esquema de asientos desde la liquidación)
- **Actualiza a:** No aplica

## Objetivo
Agregar una marca de agua al PPT y dejar una versión que el cliente no pueda modificar.

## Estado final
Terminado. Tres archivos, movidos al Escritorio (`OneDrive/Desktop`) a pedido de la usuaria:
- `... - marca de agua.pptx`: el PPT original con la marca de agua (editable).
- `....pdf`: PDF con la marca de agua (lo recomendado para mandar).
- `... - no editable.pptx`: cada diapositiva es una imagen (2560×1440) con la marca ya incorporada; no hay texto para editar.

## Decisiones y por qué
- Marca diagonal "SOFTUR · CONFIDENCIAL" en Terracota `#B7470D` con 82 % de transparencia, más una leyenda al pie en gris — usa los colores de la marca Softur y deja leer el contenido. [decisión]
- No existe un PPT "imposible de modificar": "Marcar como final" o la contraseña de escritura se sacan en segundos. Lo más firme es el PDF o el PPT de imágenes (no se puede editar el texto ni sacar la marca sin retocar la imagen). [datos]

## Archivos, tablas y objetos relevantes
- Origen: `Downloads/Esquema administrativo - contable iTRAFFIC asientos desde liquidacion (marca Softur)_2.pptx` (16 diapositivas, 16:9).
- No se consultó Softur.Serenity (la tarea era de formato, no de procesos).

## Cambios hechos
- Script PowerShell con PowerPoint por COM: agrega las formas `MarcaDeAgua` y `LeyendaConfidencial` en cada diapositiva, guarda una copia, exporta a PDF (`SaveAs` formato 32), exporta los PNG y arma una presentación nueva con una imagen por diapositiva. El original no se tocó.

## Errores y cómo se resolvieron
- No hubo errores. El script se corrió con PowerShell 7 (UTF-8), para que el "·" salga bien.

## Riesgos
- En la versión de imágenes se pierden los hipervínculos/flechas de navegación entre diapositivas y el texto no se puede buscar ni copiar.
- El PPT con la marca de agua sigue siendo editable: la marca se puede borrar. No mandarlo al cliente.

## Pendientes
- [ ] Si se quiere bloquear también impresión o copia del PDF, hace falta Acrobat u otra herramienta con permisos (la PC no tiene una) — usuaria.

## Cómo validar
- Abrir el PDF y el PPT no editable: la marca aparece en las 16 diapositivas; en el PPT no editable, al hacer clic se selecciona sólo una imagen.

## Datos que pueden quedar viejos
- Diapositivas — 16 — (foto al 2026-10-14)
