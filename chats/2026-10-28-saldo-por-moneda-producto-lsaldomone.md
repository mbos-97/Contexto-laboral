# Informe "Saldo por moneda producto" (LSALDOMONE)

**Fecha:** 2026-10-28

## Objetivo

Ver si el informe "Saldo por moneda producto" de Saldo cliente sirve para mostrar, de un cliente, lo pendiente en USD y en $ cada uno en su moneda.

## Estado final

Sí: es el informe impreso `LSALDOMONE` del listado Saldo cliente. En una sola salida muestra, por reserva, columnas **TOTAL / COBRO / SALDO** en **$, U$S y MEP**, con subtotales por cliente y total general. Corrige lo dicho en [2026-10-28-saldo-cliente-por-moneda.md](2026-10-28-saldo-cliente-por-moneda.md): ahí se había dicho que no había un informe con las dos monedas juntas. `[código]`

## Decisiones y por qué

No aplica (consulta).

## Archivos, tablas y objetos relevantes

- Alta del informe: `ScriptsBD/Sp_Configs/InformesWebDefaultInsert.sql`. Nombre `LSALDOMONE`, descripción "Saldo por moneda producto", pantalla `SALDOCLIENTELIST`, SP `iLSALDRVA_ListItraffic`, plantilla `Reports/Templates/LSALDOMONE.cshtml`. `[código]`
- Variantes por cliente: `LSALDOMONE_00165`, `_00325`, `_2102`, `_34113`, `_5093`, `_CUE`, `LSALDOGROUPMONEY_5093`. `[código]`
- Según la config **`REGISTROFACDIFMONEDAS`**, el SP calcula de dos formas distintas (`iLSALDRVA_ListItraffic.sql`, líneas ~1465-1495 y ~7300-7400) `[código]`:
  - **`= SI`** (tipocc 20). El total sale de `FMONTO_MONE_rv`: suma `det_rvah.Totall` por **`det_rva.Monedaventa`**, es decir, por la **moneda de venta de cada servicio**. Para el saldo (`fCOBRO_MONEDA_CBTE_XSALDO`) se restan los cobros imputados a facturas con `Monedaimpre` en esa moneda y los recibos sin factura de esa moneda. Una reserva con servicios en USD y en $ queda separada.
  - **Otro valor o sin config** (tipocc 21, `@SaldoMoneda = 21`). El total sale de `FMONTO_MONE_rv2`: lo **facturado** de las reservas cuya **`reserva.moneda`** es esa moneda. Los cobros salen de `fCOBRO_MONEDA_RVA_estadodecuenta`, por moneda de la reserva. Agrega MEP. Separa por moneda de la reserva, no del servicio, y cuenta lo facturado, no lo vendido.
- Config `SALDCLISINRVA = .T.`: suma los cobros sin reserva, por moneda (`fCOBRO_MONEDA_SINFILE`). `[código]`

## Cambios hechos

No aplica (sólo lectura).

## Errores y cómo se resolvieron

La memoria anterior del mismo día no había detectado este informe porque se buscaron plantillas `SALDOCLIENTE*`; el nombre real es `LSALDOMONE`.

## Riesgos

- Sin `REGISTROFACDIFMONEDAS = SI`, el total por moneda es lo **facturado**: una reserva sin facturar puede salir en 0. `[código]`
- El resultado depende de que haya cotización en `comprobcambio` para cada recibo y factura. `[código]`

## Pendientes

- Confirmar en el cliente qué valor tiene `REGISTROFACDIFMONEDAS` y probar el informe con un cliente que tenga reservas en las dos monedas. `[hipótesis]`

## Cómo validar

Saldo cliente → filtrar el cliente → imprimir "Saldo por moneda producto". Comparar SALDO $ y SALDO U$S con las corridas por moneda (Moneda Reserva + Moneda).

## Datos que pueden quedar viejos

Código al 2026-10-28.
