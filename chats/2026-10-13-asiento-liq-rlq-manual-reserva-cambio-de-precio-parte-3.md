# Asiento LIQ / RLQ manual en Caracol: ingreso del paquete en cuenta de paquetes

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — ambiente de testeo (base iTraffic Caracol)
- **Actualiza a:** [2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-2.md](2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-2.md)

## Objetivo
Rearmar los tres asientos usando la cuenta de paquetes para el ingreso del paquete.

## Estado final
Terminado. Asientos entregados; la carga manual queda a cargo de la usuaria.

## Decisiones y por qué
- El ingreso del paquete va a `4218 VENTA DE PAQ. INTERNAC. DE TERCEROS`; el resto de los ingresos sigue en `4216 VENTA DE SERVICIOS VARIOS`. `[decisión]`
- Al separar el paquete, la asistencia (venta 500, costo 600) deja de compensarse con él: su margen de −100 va al debe de `4216`, igual que hace el sistema con los importes negativos (invierte el lado). `[código]`
- Por eso los asientos totalizan 3.900 (inicial y reversión) y 4.000 (nuevo), aunque el deudor siga siendo 3.800 y 3.900. `[datos]`

## Archivos, tablas y objetos relevantes
No se consultó código ni pantallas nuevas; ver memorias anteriores.

## Cambios hechos
Ninguno en el sistema. Sólo esta memoria.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
Los mismos de la parte 2 (sin comprobantes LIQ / RLQ en Caracol; asiento manual sin vínculo a `liq_rva`).

## Pendientes
- [ ] Cargar los tres asientos en Caracol — usuaria.

## Cómo validar
Al final: `1311` en 3.900 al debe, `2121` en 2.000 al haber, `4218` en 1.600 al haber y `4216` en 300 neto al haber.

## Datos que pueden quedar viejos
- Reserva de prueba: venta 3.900, costo 2.000 — (foto al 2026-10-13)
