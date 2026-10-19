# Desdobles en la Ficha Operativa: qué son y cómo se hacen

- **Fecha:** 2026-10-19
- **Proyecto / cliente:** Softur / iTraffic — módulo Receptivo (Ficha Operativa)
- **Actualiza a:** No aplica (complementa [2026-10-15-circuito-operativo-itraffic-cuenca-del-plata.md](2026-10-15-circuito-operativo-itraffic-cuenca-del-plata.md))

## Objetivo
Explicar a la usuaria para qué sirven los desdobles de la Ficha Operativa y cómo se cargan.

## Estado final
Terminado: explicación dada en el chat en base al código. No se generó documento.

## Decisiones y por qué
- Un desdoble agrega a la reserva un servicio operativo extra (traslado de acercamiento, IN/OUT, otro móvil) para uno o varios servicios de la ficha, sin tocar el servicio vendido. `[código]`
- Se crea seleccionando filas de la ficha y usando "Nuevo desdoble para los elementos seleccionados"; también se pueden sumar filas a un desdoble existente o quitarlas. Una fila sólo puede estar en un desdoble. `[código]`
- Datos del desdoble: Servicio (de los seleccionados) y Costo del servicio (`cost_ser`, completa Categoría y Prioridad), Tipo (parame `TDLE`: IN, OUT, IN OUT, DESDOBLE `NPAX`, DESDOBLE C/SEP PAX `SPAX`), Lugar de acercamiento, Ref. lugar, Hora in / Hora out (por defecto la menor y la mayor de las filas elegidas), cantidades ADU/CHD/INF, Observación (obligatoria) y Estado (parame `EDLE`: Planificado, Aplicado, Cancelado). `[código]`
- Sólo con tipo `SPAX` se pueden editar las cantidades de pasajeros (no pueden superar la suma de las filas elegidas); con los demás tipos toma todos los pax. `[código]`
- Al grabar, por cada servicio incluido se inserta una línea nueva en la reserva (`det_rva`, marcada con `iddesdobleoriginal`) con el servicio/categoría/prioridad del desdoble, costo y venta en 0, y descripción con prefijo `--` salvo config `SHOW_DESDFICHAOP` = SI. `[código]`
- Tipo IN con lugar de acercamiento y Ref. lugar: el lugar pasa a ser el destino (info2) del servicio original; tipo OUT: pasa a ser el origen (info1). Los valores originales se guardan y se restauran al quitar el desdoble. `[código]`
- Quitar filas de un desdoble borra las líneas generadas y restaura info1/info2/vuelos; eliminar el desdoble sólo desvincula las filas. `[código]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity — `Softur.Serene.Web/Modules/J_Receptivo/Desdoble/` (`DesdobleRow.cs`, `DesdobleForm.cs`, `DesdobleDialog.ts`, `DesdobleRepository.cs`, `DesdobleEndpoint.cs`, bulk actions Add/Clear, `FindDesglose/DesdoblePikerDialog.ts`).
- `Modules/J_Receptivo/FichaOperativa/FichaOperativaGrid.ts` (botones `AddDesdoble`, `AddExDesdoble`, `RmvDesdoble`; ícono por fila nuevo/ver desdoble), `FichaOperativaRow.cs` (campo `IdDesdoble`).
- `Modules/Texts.cs` (textos de botones y validaciones), `Modules/Common/StoreProcedureKeys.cs`.
- Tablas: `desdoble`, `det_rva2` (`iddesdoble`, `iddesdobleoriginal`), `det_rva`, `det_rvah`, `det_rvac`, `det_rvao` (`info1original`, `info2original`, `vuelo1original`, `vuelo2original`), `cost_ser`, `parame` (`TDLE`, `EDLE`), `config` (`SHOW_DESDFICHAOP`, `NOLIMPIADET_RVADESDOBLADO`, `FO_RESETSEL`).
- SPs en `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/`: `iDet_rvaDesdoblaitem`, `iDet_RvaUpdateInsertxDesdoble`, `iDet_rvaUndoDesdoblaitem`, `idet_RvaDesdobleAnular`.
- Manual iTraffic indexado (`App_Data/AIAssistant/Manuals/Indexed/manuals_index.json`, pág. ~313).

## Cambios hechos
Ninguno en código. Se creó esta memoria.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- El costo de la línea generada queda en 0 en el SP; el costo real del desdoble se definiría luego en el planning/costeo. `[hipótesis]`

## Pendientes
- [ ] Confirmar con operaciones cómo se costea el móvil del desdoble (planning vs. carga manual) — usuaria.

## Cómo validar
En una base de prueba, abrir la Ficha Operativa, seleccionar dos traslados, crear un desdoble tipo IN con lugar de acercamiento y verificar que la reserva muestre la línea nueva `--<servicio>` y que el destino del traslado original cambie al lugar indicado.

## Datos que pueden quedar viejos
- Valores de `TDLE` / `EDLE` según `ParameDefault.sql` — (foto al 2026-10-19)
