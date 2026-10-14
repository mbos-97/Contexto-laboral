# Asiento LIQ manual en Caracol: reversión y asiento nuevo por 3.900

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — ambiente de testeo (base iTraffic Caracol)
- **Actualiza a:** [2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-7.md](2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-7.md)

## Objetivo
Entregar la reversión del asiento inicial (ya cargado por la usuaria) y el asiento nuevo con el precio actualizado.

## Estado final
Terminado. Asientos entregados; la carga manual queda a cargo de la usuaria.

## Decisiones y por qué
- Reversión: espejo del inicial. Debe `2214` 300, `2217` 3.000, `2216` 500; Haber `1311` 3.800. `[código]`
- Asiento nuevo: Debe `1311` 3.900; Haber `2214` 300, `2217` 3.000, `2216` 500, `2513` 100. `[decisión]`
- El ajuste de precio (100) se mandó a `2513 VENTAS X FACTURAR` porque no tiene operador ni se le paga a un proveedor; la usuaria no lo confirmó. `[hipótesis]`

## Archivos, tablas y objetos relevantes
No se consultó código ni pantallas nuevas; ver memorias anteriores.

## Cambios hechos
Ninguno en el sistema por parte de Claude. Sólo esta memoria.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
Los mismos de la parte 2.

## Pendientes
- [ ] Confirmar la cuenta del ajuste de precio — usuaria.

## Cómo validar
Después de los tres asientos: `1311` 3.900 al debe; al haber `2214` 300, `2217` 3.000, `2216` 500, `2513` 100.

## Datos que pueden quedar viejos
- Reserva de prueba: venta 3.900 — (foto al 2026-10-13)
