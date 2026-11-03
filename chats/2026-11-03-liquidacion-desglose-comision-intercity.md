# Liquidación detallada con desglose de comisión (Intercity)

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Intercity (informe "LD - Liquidacion Detalladas" de iTraffic)
- **Actualiza a:** No aplica

## Objetivo
Generar una copia de una liquidación con el recuadro de totales desglosado: bruto sin IVA, comisión, subtotal, IVA 21%, IVA 10,5% y total a pagar.

## Estado final
Terminado. PDF generado en `Entregables`; el original no se tocó. Los importes los definió la usuaria. `[decisión]`

## Decisiones y por qué
- Editar el contenido del PDF en lugar de tapar con parches — las fuentes son Helvetica estándar y el resultado queda igual al original. `[datos]`
- Importes en el formato del documento (punto decimal, sin separador de miles) y títulos sin tilde, como el resto del informe. `[decisión]`
- "TOTAL NETO A PAGAR" pasa a "TOTAL A PAGAR", como lo pidió la usuaria. `[decisión]`
- Los tres renglones nuevos entran bajando 27 pt el bloque Datos de facturación y Vencimiento, sobre el espacio libre antes de Observaciones. `[datos]`

## Archivos, tablas y objetos relevantes
- Entrada: PDF `28722.pdf` (iTextSharp, 2 páginas; la página 2 ya viene con el encabezado y una línea suelta del pie).
- Salida: `Entregables/28722 - Liquidacion con desglose de comision.pdf`.
- No se consultó Softur.Serenity: fue una edición puntual del PDF, sin cambios en el informe.

## Cambios hechos
- Página 1: recuadro de totales reemplazado y bloque inferior desplazado. Página 2 sin cambios.

## Errores y cómo se resolvieron
- Python no está instalado — se usó Perl de Git Bash (`Compress::Zlib`) para descomprimir y reescribir el contenido de la página y recalcular la tabla xref. `[datos]`

## Riesgos
- Diferencia de 0,01 en los importes indicados: 12922.22 - 587.09 da 12335.13 (figura 12335.12) y 12335.12 + 105.31 da 12440.43 (figura 12440.44). La suma de la columna TOTAL del propio informe da 12440.43; el 12440.44 ya venía en el original. `[datos]`
- El cambio es sólo en este PDF: una nueva emisión desde iTraffic vuelve al formato anterior. `[datos]`

## Pendientes
- [ ] Confirmar si la diferencia de 0,01 queda como está — usuaria.

## Cómo validar
Abrir el PDF y comparar el recuadro con los importes pedidos; el resto de la página tiene que coincidir con el original.

## Datos que pueden quedar viejos
- Importes de la liquidación — (foto al 2026-11-03)
