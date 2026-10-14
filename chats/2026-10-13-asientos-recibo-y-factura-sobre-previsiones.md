# Asientos de recibo y factura de venta sobre una reserva con previsión (Caracol)

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — ambiente de testeo (base iTraffic Caracol)
- **Actualiza a:** [2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-8.md](2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-8.md)

## Objetivo
Definir debe y haber de los asientos de recibo y de factura de venta de la reserva de prueba, que ya tiene cargado el asiento de previsión por 3.900.

## Estado final
Terminado. Asientos propuestos; la carga manual queda a cargo de la usuaria.

## Decisiones y por qué
- Recibo: Debe forma de pago (caja / banco), Haber `1311 CLIENTES`. `[decisión]`
- Factura de venta: el ingreso va al haber y la contrapartida al debe son las transitorias que dejó la previsión, no CLIENTES (que ya se debitó en la previsión). `[decisión]`
- En el sistema la factura de fee hace lo mismo: ajusta la cuenta "por facturar" (parcuent `IFR`) contra el ingreso. `[código]`
- La transitoria de IATA no se cancela con la factura de venta sino con el pago a IATA. `[decisión]`
- Se asumió criterio de ingreso bruto: la factura toma la venta completa del paquete y la asistencia, y el costo entra aparte con la factura del proveedor. `[hipótesis]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity `ScriptsBD/Sp`: `iAsiento_CreateFacturaFee.sql`, `iAsiento_CreateFacturaComision.sql` (uso de `IFR` en la factura).
- Cuentas Caracol: `1311`, `1114`, `2214`, `2216`, `2217`, `2513`, `4216`, `4218`, `4314`, `5316`, `5318`, `2111`.

## Cambios hechos
Ninguno en el sistema. Sólo esta memoria.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Si el ajuste de 100 ya se mandó a ingresos en la previsión, no debe repetirse en la factura.

## Pendientes
- [ ] Confirmar criterio de ingreso bruto o sólo margen — usuaria.

## Cómo validar
Después de recibo, factura, pago a IATA y facturas de proveedor, `1311` y todas las transitorias quedan en cero.

## Datos que pueden quedar viejos
- Reserva de prueba: venta 3.900, costo 2.000 — (foto al 2026-10-13)
