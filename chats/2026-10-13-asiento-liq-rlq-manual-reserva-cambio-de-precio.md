# Asiento LIQ / RLQ manual para una reserva con cambio de precio de venta

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — ambiente de testeo (reserva de prueba)
- **Actualiza a:** No aplica

## Objetivo
Armar los asientos a cargar a mano para una reserva de prueba en dólares, con el mismo formato que genera el sistema (LIQ + reversión RLQ): asiento inicial por 3.800 y reversión cuando la venta pasó a 3.900.

## Estado final
Terminado. Se entregaron tres asientos (LIQ 3.800, RLQ espejo 3.800, LIQ nuevo 3.900) con cuenta, debe y haber.

## Decisiones y por qué
- El asiento LIQ se arma: Debe deudor por el total de venta; Haber cuenta transitoria del operador por el costo; Haber cuenta de ingreso por la utilidad (venta − costo). `[código]`
- La reversión RLQ es el espejo exacto del LIQ original (mismas cuentas e importes, debe/haber invertidos, descripción con `*RVS*` + nro. de asiento original); después se genera un LIQ nuevo con los valores vigentes. No se asienta sólo la diferencia. `[código]`
- Se asumió que la diferencia de 100 entre 3.800 y 3.900 es el ítem "Ajuste de precio" (venta 100, costo 0, sin operador). `[hipótesis]`
- Se agruparon las líneas por operador para que el servicio con margen negativo (asistencia: venta 500, costo 600) no genere una línea de ingreso al debe y el asiento totalice 3.800. `[decisión]`
- Los números de cuenta salen del asiento de ejemplo de la usuaria; la cuenta transitoria del operador terrestre es inventada (no figura en el ejemplo). `[hipótesis]`

## Archivos, tablas y objetos relevantes
Consultado en Softur.Serenity (`Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD`):
- `Sp/iAsiento_CreateReservaIngresoxFacturarByLiq_Rva.sql` — asiento LIQ simple (deudor contra ingresos por facturar, parcuent `IFR` / `DEU` / `D2U`).
- `Sp/iAsiento_CreateReservaIngresoxFacturarByLiq_RvaReglasPrices.sql` — asiento LIQ por servicio; tipos de cuenta `FRE` (costo), `FEE`, `ING`, `COM`, `IXT`, `OIF`, resueltos por comodín (parame `CGAR`).
- `Sp/iAsiento_Reversionbyid.sql` — genera el RLQ espejo y guarda `liq_rva.idasientoreversion`.
- `Func/fsp_DameCuentaOperLiq.sql` — busca la cuenta "Transitorio" del operador (tipoparcuent `FRE`).
- Tablas: `liq_rva`, `asiento`, `mov_asto`, `det_rva`, `parcuent`, `plan_cta`, `comprobcambio`.

## Cambios hechos
Ninguno en sistemas. Sólo esta memoria.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Un asiento cargado a mano no queda vinculado a `liq_rva` (`idasiento` / `idasientoreversion`), así que el proceso automático no lo reconoce como liquidación de la reserva. `[código]`
- Las cuentas reales dependen de la configuración de comodines y parcuent de cada base.

## Pendientes
- [ ] Confirmar la cuenta transitoria real del operador terrestre en la base de testeo — usuaria.

## Cómo validar
Cada asiento debe balancear (debe = haber) y, sumados LIQ + RLQ + LIQ nuevo, el saldo del deudor debe quedar en 3.900 y el transitorio de operadores en 2.000.

## Datos que pueden quedar viejos
- Reserva de prueba: venta 3.900, costo 2.000, moneda dólares — (foto al 2026-10-13)
