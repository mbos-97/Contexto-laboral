# Transfer IN de madrugada: cómo lo resuelve Caracol (datos reales)

- **Fecha:** 2026-11-13
- **Proyecto / cliente:** Caracol (iTraffic receptivo, Iguazú)
- **Actualiza a:** [2026-11-13-transfer-in-vuelo-cruza-medianoche-parte-2.md](2026-11-13-transfer-in-vuelo-cruza-medianoche-parte-2.md)

## Objetivo
Ver en la Ficha Operativa de Caracol cómo cargan los TRF IN con vuelos que llegan pasada la medianoche y para qué usan las reservas "HORARIOS".

## Estado final
Terminado: relevado en sólo lectura sobre la ficha operativa del 01/10 al 31/12/2026.

## Decisiones y por qué
- Caracol carga el TRF IN con **fecha del día de llegada** (el día después de la medianoche) y hora 00:xx (ej. 00:10, 00:20, 00:35). El IN y el OUT del ítem quedan iguales. [datos]
- El planning de esos ítems queda ese mismo día, con hora desde y hora hasta = hora de llegada. No los mueven al día anterior. [datos]
- Vuelos: en algunos casos cargan hora de salida = hora de llegada (ej. `H00:20 H00:20`), así no se dispara el +1 día de la asociación automática. [datos]
- En un caso el mismo planning tiene un ítem del día anterior y el de las 00:20 (hora desde 00:20, hora hasta 11:20): no queda prolijo. [datos]
- Reservas "HORARIOS": agencia/cliente HORARIOS, una reserva por período, categorías REG/ADIC. Sus ítems son servicios ficticios: "HORARIO DE CHOFER" (`HC-HORARIO DEL CONDUCTOR`) y "HORARIO DE G U I A" (`HG-HORARIO DEL GUIA`), además de inspecciones municipales/provinciales. Cada ítem lleva fecha, hora de inicio, chofer/guía y vehículo, y tiene su propio planning. Sirven para marcar en la ficha a qué hora arranca cada chofer o guía. Hay ítems a las 23:00 / 23:59 del día anterior. [datos]
- No se encontró una relación explícita entre un HORARIO de las 23:xx y un TRF IN de las 00:xx del día siguiente. Los choferes de los IN de madrugada no tenían ítem de HORARIO en el período. [datos]
- Recomendación para el caso 31/12 23:30 → 01/01 00:05: TRF IN con fecha 01/01 y hora 00:05 (el vuelo se asocia solo y la tarifa no cambia). Además, un ítem "HORARIO DE CHOFER" en la reserva HORARIOS con fecha 31/12 y hora 23:30, asignado al mismo chofer y vehículo, para que en la ficha del 31 figure la salida. [decisión pendiente de la usuaria]

## Archivos, tablas y objetos relevantes
- Pantalla: `J_Receptivo/FichaOperativa` de Caracol; servicio `Services/J_Receptivo/FichaOperativa/List` (sólo lectura).
- Campos: `Fecha`, `In`, `Out`, `Hora`, `Horavue`, `Vuelo1`, `Idbloqueo`, `HoraDesde`, `HoraHasta`, `Descripcomodin`.
- Reservas de horarios con cliente HORARIOS (una por período).

## Cambios hechos
No aplica (consulta en sólo lectura).

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Si el chofer sale el día anterior y sólo se carga el TRF el día siguiente, la ficha del día anterior no lo muestra, salvo que se agregue el ítem de HORARIO.

## Pendientes
- [ ] Confirmar con Caracol si usan el HORARIO DE CHOFER para las salidas nocturnas — usuaria.

## Cómo validar
En la Ficha Operativa de Caracol, filtrar el día de un IN de madrugada y el día anterior, y ver si aparece el HORARIO del chofer.

## Datos que pueden quedar viejos
- 7 TRF con vuelo entre 00:01 y 04:59, y 1.244 ítems HORARIOS del 01/10 al 31/12/2026 — (foto al 2026-11-13).
