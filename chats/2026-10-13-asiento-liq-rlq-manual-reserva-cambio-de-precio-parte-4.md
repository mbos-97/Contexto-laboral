# Asiento LIQ / RLQ manual en Caracol: ingreso del aéreo en cuenta de transporte aéreo

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — ambiente de testeo (base iTraffic Caracol)
- **Actualiza a:** [2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-3.md](2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-3.md)

## Objetivo
Rearmar los tres asientos usando la cuenta de transporte aéreo para el ingreso del aéreo.

## Estado final
Terminado. Asientos entregados; la carga manual queda a cargo de la usuaria.

## Decisiones y por qué
- Ingreso por servicio: aéreo en `4212 VENTA SERV.DE TRANSPORTE AEREO`, paquete en `4218 VENTA DE PAQ. INTERNAC. DE TERCEROS`, asistencia y ajuste de precio en `4216 VENTA DE SERVICIOS VARIOS`. `[decisión]`
- La asistencia (margen −100) sigue al debe de `4216`; los totales no cambian respecto de la parte 3 (3.900 / 3.900 / 4.000). `[datos]`

## Archivos, tablas y objetos relevantes
No se consultó código ni pantallas nuevas; ver memorias anteriores.

## Cambios hechos
Ninguno en el sistema. Sólo esta memoria.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
Los mismos de la parte 2.

## Pendientes
- [ ] Cargar los tres asientos en Caracol — usuaria.

## Cómo validar
Al final: `1311` en 3.900 al debe; al haber `2121` 2.000, `4212` 300, `4218` 1.600; `4216` en cero neto (100 debe de asistencia, 100 haber del ajuste).

## Datos que pueden quedar viejos
- Reserva de prueba: venta 3.900, costo 2.000 — (foto al 2026-10-13)
