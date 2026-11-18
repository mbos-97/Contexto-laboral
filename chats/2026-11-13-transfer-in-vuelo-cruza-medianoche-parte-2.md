# Transfer IN con IN 31/12 y OUT 01/01: efecto en reserva y tarifa

- **Fecha:** 2026-11-13
- **Proyecto / cliente:** iTraffic receptivo (consulta general)
- **Actualiza a:** [2026-11-13-transfer-in-vuelo-cruza-medianoche.md](2026-11-13-transfer-in-vuelo-cruza-medianoche.md)

## Objetivo
Evaluar qué pasa si el TRF IN se carga con IN 31/12 y OUT 01/01 (en lugar de IN = OUT).

## Estado final
Terminado: no conviene; el OUT no resuelve la asociación del vuelo y puede duplicar la tarifa.

## Decisiones y por qué
- En el ítem de la reserva, cambiar IN/OUT recalcula `Nts = OUT - IN` (queda 1) y dispara el recosteo. [código]
- Tarifa de servicio (`icost_ser_GetDetRva`): `@noches = DATEDIFF(IN, OUT)`; si `tip_serv.dias = 1` suma 1; si da 0 pasa a 1; si `servicio.pago = 'T'` fuerza 1; si `servicio.pago = 'D'` suma 1. El precio y el costo por pax se multiplican por `@noches`. [código]
  - `pago = 'T'`: cobra 1 vez (sin impacto).
  - `pago = 'D'`: con IN 31 / OUT 01 cobra **2** (con IN = OUT cobra 1).
  - Otro valor: cobra 1, salvo que el tipo de servicio tenga `dias = 1`, que da 2.
  - Con más de una noche la tarifa se arma por fecha (`@nochesserv`): si 31/12 y 01/01 tienen tarifas o vigencias distintas (fin de año), puede tomar dos tarifas o fallar por falta de tarifa el 01/01. [hipótesis]
- Asociación del vuelo (`iReserva_AsociarTrfSmart`): las uniones usan sólo `det_rva.in_`, no el OUT, así que el OUT 01/01 no hace que el vuelo se asocie solo. [código]
- La Ficha Operativa tiene `Fecha` y `FechaFin`; si el filtro por día también trae ítems por fecha fin (y el servicio aparece el 01/01) no se verificó. [hipótesis]
- Recomendación: dejar IN = OUT = 31/12, hora 23:30, y asociar el vuelo a mano. [decisión pendiente de la usuaria]

## Archivos, tablas y objetos relevantes
- `Softur.Serene.Model/.../ScriptsBD/Sp/icost_ser_GetDetRva.sql` (cálculo de `@noches`, `servicio.pago`, `tip_serv.dias`).
- `Softur.Serene.Model/.../ScriptsBD/Sp/iCostoTra_GetDetRva.sql` (tarifa de traslados con `costotra`: `@noches = 1` fijo; `nts` y `can_dias` informativos).
- `Softur.Serene.Web/Modules/E_Ventas/Det_pres/Det_presEditorDialog.ts` (cambio de IN/OUT → `Nts` → `recosteoProcess`).
- `Softur.Serene.Web/Modules/E_Ventas/Det_rva/Det_rvaService.generated.cs` (`CostoSerGetDetRva`, `CostoTraGetDetRva`).
- Tablas: `det_rva`, `servicio` (`pago`), `tip_serv` (`dias`), `cost_ser`, `costotra`.

## Cambios hechos
No aplica (consulta).

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Servicios con `pago = 'D'` o tipo con `dias = 1`: precio y costo duplicados.
- Tarifas distintas para el 01/01 (feriado / fin de año).

## Pendientes
- [ ] Ver en el maestro de servicio el valor de `pago` del transfer y `dias` de su tipo — usuaria.
- [ ] Verificar si la Ficha Operativa del 01/01 muestra el ítem por `FechaFin` — usuaria.

## Cómo validar
En una base de prueba, cargar el TRF con IN 31/12 / OUT 01/01 y comparar el total con el mismo ítem en IN = OUT.

## Datos que pueden quedar viejos
- Lógica de los SP — foto al 2026-11-13.
