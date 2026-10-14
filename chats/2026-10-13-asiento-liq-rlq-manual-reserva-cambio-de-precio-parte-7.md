# Asiento LIQ manual en Caracol: cada servicio por su venta total a una transitoria

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — ambiente de testeo (base iTraffic Caracol)
- **Actualiza a:** [2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-6.md](2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-6.md)

## Objetivo
Rearmar el asiento inicial con el criterio definido por la usuaria y las cuentas transitorias que creó.

## Estado final
Terminado. Asiento inicial entregado; la carga manual queda a cargo de la usuaria.

## Decisiones y por qué
- Cada servicio va por su **venta total** a una cuenta transitoria de pasivo según el tipo de servicio, sin separar costo y margen: después se netea con los comprobantes (pago a IATA, facturas). `[decisión]`
- Aéreo → `2214 IATA TRANSITORIO` por el total del ticket (300). `[decisión]`
- Paquete → `2217 VENTA PAQUETES TRANSITORIOS` (3.000); asistencia → `2216 ASISTENCIAS INTERNACIONALES TRANSITORIAS` (500). `[decisión]`
- La usuaria creó en Caracol las cuentas `2215 OPERADORES TRANSITORIO`, `2216`, `2217` y `2513 VENTAS X FACTURAR`. `[datos]`
- Con este criterio ya no hace falta netear el margen negativo de la asistencia: el asiento totaliza 3.800 naturalmente. `[datos]`

## Archivos, tablas y objetos relevantes
- Pantalla consultada (sólo lectura): `H_Contabilidad/Plan_cta`.
- No se consultó código nuevo de Softur.Serenity.

## Cambios hechos
Ninguno en el sistema por parte de Claude. Sólo esta memoria.

## Errores y cómo se resolvieron
- La parte 6 separaba costo (transitorio) y margen (por facturar) — el criterio correcto es venta total por tipo de servicio — corregido acá.

## Riesgos
Los mismos de la parte 2.

## Pendientes
- [ ] Definir a qué cuenta va el ajuste de precio de 100 en el asiento nuevo — usuaria.
- [ ] Cargar los asientos — usuaria.

## Cómo validar
Asiento inicial: Debe `1311` 3.800; Haber `2214` 300, `2217` 3.000, `2216` 500.

## Datos que pueden quedar viejos
- Cuentas `2215`, `2216`, `2217`, `2513` existentes en Caracol — (foto al 2026-10-13)
