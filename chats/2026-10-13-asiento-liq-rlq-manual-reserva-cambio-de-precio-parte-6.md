# Asiento LIQ / RLQ manual: es un asiento de previsión, no toca resultados

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — ambiente de testeo (base iTraffic Caracol)
- **Actualiza a:** [2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-5.md](2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-5.md)

## Objetivo
Corregir la lógica de los asientos: las versiones anteriores mandaban la utilidad a cuentas de resultado y eso está mal.

## Estado final
Terminado. Asientos rearmados sólo con cuentas patrimoniales; quedan dos cuentas a crear por la usuaria.

## Decisiones y por qué
- El asiento LIQ de la reserva es de previsión: Debe deudor por la venta; Haber cuentas patrimoniales (transitorio del operador por el costo, "por facturar" por el resto). Las cuentas de resultado se toman después, al cargar los comprobantes (factura de venta, factura de proveedor) que netean esas previsiones. `[decisión]`
- Lo único que el LIQ manda directo a ganancias son los fees de intermediación (en el asiento de referencia: "Otros ingresos por intermediación y Fee"). `[decisión]`
- La reserva de prueba no tiene ítems de fee de intermediación, así que sus asientos no tocan ninguna cuenta de resultado. `[hipótesis]`
- En Caracol faltan dos cuentas de pasivo: una de ventas / ingresos por facturar y una transitoria de operadores. Parámetros Cuentas tampoco tiene fila `IFR` (ingresos por facturar). `[datos]`
- Propuesta de alta: `2513 VENTAS POR FACTURAR` y `2215 OPERADORES TRANSITORIO` (números libres en el plan). Sin alta, las más cercanas son `2511 ANTICIPOS DE CLIENTES` y `2121 PREVISIONES`. `[hipótesis]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity: `Sp/iAsiento_CreateReservaIngresoxFacturarByLiq_Rva.sql` (versión simple: deudor contra parcuent `IFR`, sin resultados). `[código]`

## Cambios hechos
Ninguno en el sistema. Se marcó como histórica la regla anterior en `PROJECT_MEMORY.md`.

## Errores y cómo se resolvieron
- Las partes 1 a 5 imputaban la utilidad a cuentas de ingreso (`4212`, `4216`, `4218`) — se leyó el margen del asiento de referencia como resultado cuando sólo los fees lo son — corregido en esta memoria.

## Riesgos
Los mismos de la parte 2.

## Pendientes
- [ ] Crear las dos cuentas en Caracol (o confirmar otras) — usuaria.
- [ ] Cargar los asientos — usuaria.

## Cómo validar
Ninguna línea de los tres asientos usa cuentas 4xxx ni 5xxx. Al final: deudor 3.900 al debe; transitorio operadores 2.000 y ventas por facturar 1.900 al haber.

## Datos que pueden quedar viejos
- Números `2513` y `2215` libres en el plan de Caracol — (foto al 2026-10-13)
