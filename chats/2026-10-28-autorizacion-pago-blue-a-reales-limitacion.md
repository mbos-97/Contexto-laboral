# Autorización de pago en reales de un ítem en dólar blue: limitación del SP

**Fecha:** 2026-10-28

## Objetivo

Seguir con [sólo trae reservas en reales](2026-10-28-autorizacion-pago-solo-trae-reales.md). Caso concreto: reserva en dólar blue, ítem con costo en **Blue [B]**, autorización en **Reales [R]**. La balanza de la AUT muestra tasas con origen REALES: R→P 0,187265; R→B 0,1872659; R→D 0,1941747; R→E 0,36764706; R→G 4763,2; R→R 1. `[datos]` (captura de la usuaria)

## Estado final

Con la AUT en reales, **el SP no puede generar la conversión Blue → Reales**, así que el ítem en blue nunca aparece. Es una limitación del código, no un problema de carga. Hay un camino alternativo para probar y un pedido a desarrollo pendiente. `[código]`

## Decisiones y por qué

No aplica (pendiente de decisión de la usuaria).

## Archivos, tablas y objetos relevantes

- `ComprobateHelper.tasasToXml`: el XML sólo manda `<moneda>` = moneda destino y `<cambio>`; **no manda la moneda origen**. `[código]`
- `iLSALDPROV_ForOPA_FPP_Itraffic.sql`, armado de `@comprobcambio`: toma **cada fila del XML como Dólar → moneda** (`'D' as moneda`). Las tasas con origen REALES se interpretan como si fueran desde el dólar. `[código]`
- Combinaciones: X → X = 1, X → D = 1/c, y X → Y sólo si **D → Y tiene cambio ≠ 1** (`c5.cambio<>1`). La fila R→R = 1 queda como D→R = 1, así que **nunca se genera B→R** (ni P→R ni E→R). Con `@moneda = 'R'` sólo entran ítems en R (R→R) y en D (D→R con cambio 1, que además está mal). `[código]`
- Hay un ajuste especial para Blue/Oficial sólo cuando la AUT es en **pesos** (`IF @moneda='P' AND exists monedas 'B'/'O'`). Para reales no existe. `[código]`
- Que la balanza muestre origen REALES sugiere la config `LCAMBIORECIBOXMONEDA = .T.` (tasas desde la moneda del comprobante). `[hipótesis]`

## Cambios hechos

No aplica (repo de sólo lectura).

## Errores y cómo se resolvieron

No aplica.

## Riesgos

- Truco posible, sin probar: escribir en la balanza tasas "por dólar" y poner en R→R un valor ≠ 1. Así el SP armaría B→R = (1/cB)·cR, pero el comprobante quedaría con tasas mal guardadas para contabilidad. No recomendado. `[hipótesis]`

## Pendientes

- Probar el camino alternativo: AUT en **Blue** (el ítem aparece por B→B = 1) y pagarla después con una OP en reales. `[hipótesis]`
- Pedido a desarrollo: que `iLSALDPROV_ForOPA_FPP_Itraffic` (y el XML de tasas) respete la moneda origen de las tasas o genere las combinaciones cuando la AUT no es en pesos ni en dólares.

## Cómo validar

Nueva AUT en Blue → mismo operador → agregar reserva: tiene que aparecer el ítem en blue.

## Datos que pueden quedar viejos

Código al 2026-10-28.
