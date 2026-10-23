# Nota de crédito con asientos desde la liquidación (LIQ): circuito con transitoria

- **Fecha:** 2026-10-23
- **Proyecto / cliente:** Softur — consulta general (iTraffic / Serenity)
- **Actualiza a:** [2026-10-23-asiento-nota-de-credito-vs-factura-venta.md](2026-10-23-asiento-nota-de-credito-vs-factura-venta.md)

## Objetivo
Explicar cómo funcionan factura y nota de crédito cuando el cliente contabiliza desde la liquidación de la reserva, con el ingreso a una transitoria.

## Estado final
Terminado (análisis de código, sin prueba en base).

## Decisiones y por qué
- En el LIQ el ingreso va a una transitoria, no a resultados. [decisión]
- LIQ básico (`iAsiento_CreateReservaIngresoxFacturarByLiq_Rva`): Debe deudores (`parcuent DEU`, o `D2U` si el cliente no tiene cuenta corriente) / Haber transitoria "ingreso por facturar" (`parcuent IFR`) por el total de los servicios (`det_rvah.total`). Si se reliquida, asienta sólo la diferencia contra lo ya generado. Con `config ASIENTOBYDESGLOSEPRICE` usa `..._RvaReglasPrices` (transitorias por tipo, `CMF`; RLQ espejo + LIQ nuevo con `LASIENTOREVERSIONLIQ_RVA`). [código]
- Factura con LIQ (`parame ASFA = DIFINGRESO` → `iAsiento_CreateFacturaFee` / `iAsiento_CreateFacturaComision`): arma el asiento normal y luego borra la línea de deudores (ya la debitó el LIQ) y la reemplaza por la transitoria (`IFR`, o en comisión la cuenta `CMF` del último LIQ). Queda: Debe transitoria / Haber ingreso (+ IVA). Este reemplazo depende de `config LFAC_PROVPORDIRECTO`. [código]
- `iAsiento_CreateFacturaComision` no asienta si la reserva no tiene LIQ con asiento; para reservas `CM` exige una sola LIQ activa y que el total de la factura coincida con ella (errores 52113 / 52114). [código]
- La N/C usa los mismos SP con `Suma_ccc = 0`: Debe ingreso (+ IVA) / Haber transitoria. Devuelve el saldo a la transitoria; el deudor del LIQ sigue abierto. [código]
- Para cerrar todo en una anulación: N/C + reliquidación/reversión (RLQ: Debe transitoria / Haber deudores). Si la venta sigue con otro precio, la transitoria queda con saldo hasta la nueva factura. [hipótesis]

## Archivos, tablas y objetos relevantes
- `ScriptsBD/Sp/`: `iAsiento_CreateSegunComprobante.sql` (rama `LIQ`), `iAsiento_CreateReservaIngresoxFacturarByLiq_Rva.sql`, `iAsiento_CreateReservaIngresoxFacturarByLiq_RvaReglasPrices.sql`, `iAsiento_CreateReservaCostoxFacturarByLiq_Rva.sql`, `iAsiento_CreateFacturaFee.sql`, `iAsiento_CreateFacturaComision.sql`.
- Tablas `Liq_rva`, `det_rvah`, `mov_asto` (`tipoparcuent`), `parcuent` (`DEU`, `D2U`, `IFR`, `CMF`), `config`.

## Cambios hechos
No aplica.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- La validación de reservas `CM` compara el total del comprobante con el LIQ activo sin mirar si es N/C: una N/C sobre una reserva CM podría ser rechazada con el error 52114. [hipótesis]

## Pendientes
- [ ] Probar en base de testeo una N/C sobre reserva con LIQ (y una reserva CM) — usuaria / implementación.

## Cómo validar
Reserva de prueba: LIQ → factura → N/C total → reliquidación. Deudores y la transitoria deben quedar en cero.

## Datos que pueden quedar viejos
No aplica.
