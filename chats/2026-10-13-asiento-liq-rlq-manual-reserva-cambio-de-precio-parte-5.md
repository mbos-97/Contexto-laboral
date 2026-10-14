# Asiento LIQ / RLQ manual en Caracol: totales 3.800 y 3.900

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — ambiente de testeo (base iTraffic Caracol)
- **Actualiza a:** [2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-4.md](2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-4.md)

## Objetivo
Que el asiento inicial totalice 3.800 y el posterior al cambio de precio 3.900.

## Estado final
Terminado. Asientos entregados; la carga manual queda a cargo de la usuaria.

## Decisiones y por qué
- Los asientos deben totalizar igual que la venta de la reserva (3.800 y 3.900), sin líneas de ingreso al debe. `[decisión]`
- Para lograrlo, el margen negativo de la asistencia (−100) se netea contra el ingreso del paquete, que es del mismo operador: `4218` queda en 1.500 en lugar de 1.600. `[decisión]`
- Cuentas finales: `1311` deudor, `2214` IATA transitorio, `2121` costo operador, `4212` ingreso aéreo, `4218` ingreso paquete (neto de asistencia), `4216` ajuste de precio. `[decisión]`
- Se interpretó que "la reversión por 3.900" es el asiento nuevo posterior al cambio; el espejo del asiento inicial totaliza 3.800 porque replica sus importes. `[hipótesis]`

## Archivos, tablas y objetos relevantes
No se consultó código ni pantallas nuevas; ver memorias anteriores.

## Cambios hechos
Ninguno en el sistema. Sólo esta memoria.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
Los mismos de la parte 2.

## Pendientes
- [ ] Cargar los asientos en Caracol — usuaria.

## Cómo validar
Al final: `1311` en 3.900 al debe; al haber `2121` 2.000, `4212` 300, `4218` 1.500, `4216` 100.

## Datos que pueden quedar viejos
- Reserva de prueba: venta 3.900, costo 2.000 — (foto al 2026-10-13)
