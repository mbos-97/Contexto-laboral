# Propuesta comercial TODO WAY VIAJES reformulada

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** TODO WAY VIAJES — iTRAFFIC Backoffice Business
- **Actualiza a:** No aplica

## Objetivo
Reformular la redacción de la propuesta comercial y dejar Inversión y Forma de pago en la misma página.

## Estado final
Parcial: documento terminado en 6 páginas (antes 8); falta definir el valor de la hora adicional antes de enviarlo.

## Decisiones y por qué
- Se mantienen todas las condiciones comerciales (USD 1.200 de setup, USD 150 de abono, 40 hs, 120 días, 3 licencias, vigencia 30 días); sólo cambia la redacción. [decisión]
- Se quita la frase "el valor de la hora adicional figura en la sección de Inversión": esa sección no informa ningún valor y no se inventa un precio. [datos]
- "Soporte y Niveles de Servicio" pasa a "Soporte": la sección no define niveles de servicio. [datos]
- Se escribe siempre "cliente" (no "comprador") y "Mesa de Ayuda" (no "mesa de soporte"). [decisión]
- El original no se toca; la versión nueva se guarda en Entregables. [decisión]

## Archivos, tablas y objetos relevantes
- Original: `Desktop/CLIENTES/TODO WAY/Propuesta_Comercial_TODO WAY VIAJES.docx`.
- Nueva versión: `Trabajo/Entregables/Propuesta_Comercial_TODO WAY VIAJES v2.docx`.
- Softur.Serenity: no se consultó; no se agregaron datos de producto.

## Cambios hechos
- 38 textos reformulados.
- "Forma de pago" tenía un salto de página propio (`pageBreakBefore`), que se quitó; Inversión, Forma de pago y Confidencialidad quedan en la página 6.
- Alcance pasa a continuación de Objetivo, sin salto.
- Tablas al ancho de la caja de texto; encabezado "Seguimiento" en la columna vacía de Soporte; encabezado de Soporte en Tinta; enlace con la tipografía del documento; se quitó un punto suelto.

## Errores y cómo se resolvieron
- Word por COM se colgaba con `ExportAsFixedFormat` — causa no determinada — exportar con `SaveAs2([string]$pdf, 17)` y pasar la ruta como `[string]`. [datos]

## Riesgos
- "Migración de datos" figura en Objetivo pero no en "Incluido en el Setup". [datos]
- "Incluido en el Setup" menciona soporte sólo por mail, mientras que la tabla de Soporte suma WhatsApp. [datos]

## Pendientes
- [ ] Definir el valor de la hora adicional y agregarlo en Inversión — usuaria.
- [ ] Confirmar si la migración de datos está incluida — usuaria.
- [ ] Confirmar si el WhatsApp de soporte entra en lo incluido — usuaria.

## Cómo validar
Abrir el .docx en Word: 6 páginas, con Inversión y Forma de pago juntas en la última.

## Datos que pueden quedar viejos
- Setup USD 1.200, abono USD 150, sin IVA — (foto al 2026-11-03)
- Versión 1.0, válida hasta 03/12/26 — (foto al 2026-11-03)
