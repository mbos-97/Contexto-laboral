# ¿Una OP en reales trae una autorización en dólar blue?

**Fecha:** 2026-10-28

## Objetivo

Seguir con [limitación Blue→Reales](2026-10-28-autorizacion-pago-blue-a-reales-limitacion.md). La usuaria pregunta si el camino alternativo (AUT en Blue + OP en reales) choca con la misma limitación al traer la AUT desde la OP.

## Estado final

La rama de la OP es distinta: trae la AUT aunque no exista el par B→R, pero **el importe convertido puede salir mal** (cambio 1). Lo más seguro es hacer la **OP en Blue** y pagar con forma de pago en reales. Sin probar. `[código]` / `[hipótesis]`

## Decisiones y por qué

No aplica.

## Archivos, tablas y objetos relevantes

- `Mov_ordOPEditor.ts`: "agregar" en la OP llama a `iLSALDPROV_ForOPA_FPP_Itraffic` con `tipocc` 6 (autorizaciones), `moneda` de la OP y `xmlcambio`. Las formas de pago por moneda salen de `showMonedasFpDilaog` / `LSALDPROV_ForOPA_Get_Creditos`. `[código]`
- SP, rama `@tipocc = 6` (línea ~1710): `inner join autoriza a1` + `inner join @comprobcambio cbio on cbio.monedadestino=@moneda`. La condición `cbio.moneda=a1.moneda` está **comentada**, así que no exige el par moneda AUT → moneda OP. `[código]`
- `fsp_SaldoAutorizacionvspago`: `@lcambioaplicar = isnull(@cambioaplicar, Comprobcambio.cambio de la AUT con destino = moneda de la OP)`. Como el SP le pasa `cbio.cambio` (no nulo, por ejemplo 1 en R→R o D→R), **no usaría la tasa guardada en la AUT**: el saldo de una AUT en blue podría salir en reales al cambio 1. `[hipótesis]` (lectura del código, no probado)

## Cambios hechos

No aplica.

## Errores y cómo se resolvieron

No aplica.

## Riesgos

- OP en reales trayendo una AUT en blue: el importe puede salir mal convertido. Verificar antes de confirmar. `[hipótesis]`

## Pendientes

- Probar: AUT en Blue → OP en **Blue** con forma de pago en reales. Alternativa: OP en reales trayendo la AUT, controlando el importe.
- Pedido a desarrollo (sigue abierto): conversiones entre monedas que no son pesos ni dólar en AUT y OP.

## Cómo validar

En la OP, al traer la AUT, comparar el importe con: importe en blue × tasa Blue→Reales.

## Datos que pueden quedar viejos

Código al 2026-10-28.
