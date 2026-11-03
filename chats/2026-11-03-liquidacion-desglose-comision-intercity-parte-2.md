# Liquidación Intercity v2: sin precios por servicio

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Intercity (informe "LD - Liquidacion Detalladas" de iTraffic)
- **Actualiza a:** [2026-11-03-liquidacion-desglose-comision-intercity.md](2026-11-03-liquidacion-desglose-comision-intercity.md)

## Objetivo
Generar una versión 2 de la liquidación con desglose, sin los precios de cada servicio.

## Estado final
Terminado. PDF generado en `Entregables`; la versión 1 sigue disponible.

## Decisiones y por qué
- Se quitan las columnas TOT S/IMP, COMISION, TASA 0, TASA 21, TASA 10.5 y TOTAL, con títulos, según el recuadro marcado por la usuaria. `[decisión]`
- Los importes se eliminan del contenido del PDF, no se tapan: no se pueden seleccionar ni copiar. `[datos]`
- Los títulos de esas columnas también se quitan del encabezado de la página 2, por coherencia. `[decisión]`
- Se mantienen el recuadro de totales y Datos de facturación, que no estaban marcados. `[decisión]`

## Archivos, tablas y objetos relevantes
- Entrada: `Entregables/28722 - Liquidacion con desglose de comision.pdf`.
- Salida: `Entregables/28722 - Liquidacion con desglose de comision v2 sin precios.pdf`.
- No se consultó Softur.Serenity: fue una edición puntual del PDF.

## Cambios hechos
- 78 textos quitados en la página 1 (6 títulos y 72 importes) y 6 títulos en la página 2. `[datos]`

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- La diferencia de 0,01 de la versión 1 sigue en esta versión. `[datos]`
- Datos de facturación todavía muestra importes globales por tipo de gravamen, y la comisión total queda visible en el recuadro. `[datos]`

## Pendientes
- [ ] Confirmar si la diferencia de 0,01 queda como está — usuaria.

## Cómo validar
Abrir el PDF: la tabla de servicios termina en PAX y el recuadro de totales coincide con la versión 1.

## Datos que pueden quedar viejos
- Importes de la liquidación — (foto al 2026-11-03)
