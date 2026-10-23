# Asiento contable de la nota de crédito y cómo netea con la factura de venta

- **Fecha:** 2026-10-23
- **Proyecto / cliente:** Softur — consulta general (iTraffic / Serenity)
- **Actualiza a:** No aplica (complementa [2026-10-13-asientos-recibo-y-factura-sobre-previsiones.md](2026-10-13-asientos-recibo-y-factura-sobre-previsiones.md))

## Objetivo
Saber qué asiento genera hoy una nota de crédito de venta y cómo se compensa con el de la factura.

## Estado final
Terminado (sólo análisis de código).

## Decisiones y por qué
- La N/C es un comprobante de la misma tabla `Factura` con `Tipo_comp = 'N/C'`; pasa por el mismo `iAsiento_CreateSegunComprobante` (rama `FAC`) y los mismos SP que la factura. No hay un SP propio de N/C. [código]
- El lado (debe/haber) sale de `Comprob.Suma_ccc`: `FAC` = 1, `N/C` = 0 (`N/D` = 1). Con 1: deudor al Debe y el resto al Haber; con 0 todo se invierte. [código]
- Los importes del detalle se multiplican por -1 si es N/C (y en el SP de costo los negativos se pasan al lado contrario en valor absoluto). Se infiere que el detalle de la N/C se guarda en negativo. [hipótesis]
- Resultado: el asiento de la N/C es el espejo del de la factura, con las mismas cuentas (`parcuent`: `DEU`, `RI`, `RNI`, `IC7`, `IC9`, `RIB`, ingreso, `COS`, `FRE`, `IFR`, `DES`, `IPR`/`ITE`). No referencia a la factura original: netea por saldo de cuenta. La compensación con el cliente es en cuenta corriente (`Resta_ccc` = 1). [código]
- Qué SP arma el asiento según `parame ASFA`: `COSTO` → `iAsiento_CreateFacturaventa` (venta por línea) + `iAsiento_CreateFacturacosto` (Debe `COS` / Haber `FRE`, salvo `config ASTOSINPREV`); `DIFINGRESO` → `iAsiento_CreateFacturaFee` (si `facturafee=1`, contra `IFR`) o `iAsiento_CreateFacturaComision` (contra `CMF`); otro → `iAsiento_CreateFactura` (costo por línea a la cuenta del detalle + ingreso por diferencia). [código]

## Archivos, tablas y objetos relevantes
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/`: `iAsiento_CreateSegunComprobante.sql`, `iAsiento_CreateFactura.sql`, `iAsiento_CreateFacturaventa.sql`, `iAsiento_CreateFacturacosto.sql`, `iAsiento_CreateFacturaFee.sql`, `iAsiento_CreateFacturaComision.sql`.
- `ScriptsBD/DataDefault/ComprobDefault.sql` (`Suma_ccc` / `Resta_ccc` de `FAC`, `N/C`, `N/D`).
- Tablas `Factura`, `Fac_det`, `Comprob`, `parcuent`, `parame` (`ASFA`), `mov_asto`.

## Cambios hechos
No aplica.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Una N/C parcial sólo netea la parte acreditada; si las cuentas del detalle de la N/C no son las mismas que las de la factura, el neteo por cuenta no cierra. [hipótesis]

## Pendientes
No aplica.

## Cómo validar
En una base de prueba: emitir factura y N/C total de la misma reserva y ver en `mov_asto` que cada cuenta queda con saldo 0.

## Datos que pueden quedar viejos
No aplica.
