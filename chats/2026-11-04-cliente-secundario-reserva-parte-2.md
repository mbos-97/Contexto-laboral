# Cliente secundario: recibos y cuenta corriente

- **Fecha:** 2026-11-04
- **Proyecto / cliente:** Softur / iTraffic (transversal)
- **Actualiza a:** [2026-11-04-cliente-secundario-reserva.md](2026-11-04-cliente-secundario-reserva.md)

## Objetivo
Saber a nombre de quién quedan los recibos de una reserva con cliente secundario y qué cuenta corriente bajan.

## Estado final
Terminado como análisis de código; no se probó en una base. El comportamiento actual no cumple lo que la usuaria espera: el recibo baja la cuenta del principal, no la del secundario.

## Decisiones y por qué
- Al elegir la reserva, `ReciboDialog.ts` pone en el recibo el `cod_agcia` que devuelve `iLSALDRVA_ForReciboItraffic`, que es `re.cod_agcia`: el principal. [código]
- Buscar por el secundario sólo trae la reserva con `LCANTREGISTROFAC = .T.` (por reserva, `tipocc = 1`); aun así, el recibo pasa al principal. [código]
- `fsp_SaldoReserva` calcula el saldo por `idreserva`, sin mirar el cliente. [código]
- `iLSALDRVA_ListItraffic`: por reserva filtra facturas y recibos por `re.Cod_agcia`; por comprobante (`tipocc` 2 y 5), por `factura.Cod_agcia` y `recibo.Cod_agcia`. El secundario no se usa como filtro: la deuda queda en el principal. [código]
- `iAsiento_CreateRecibo` toma cliente y `Ctacte` de `recibo.cod_agcia`. [código]
- Que factura, recibo y saldo queden en el secundario requiere desarrollo. Cambiar sólo el recibo dejaría la factura en el principal y el crédito en el secundario. [hipótesis]
- Sin desarrollo, si quien debe y paga es el secundario, se lo carga como cliente principal de la reserva. [hipótesis]

## Archivos, tablas y objetos relevantes
Softur.Serenity, commit `3914239c72`:
- `Softur.Serene.Web/Modules/F_Clientes/Recibo/ReciboDialog.ts` (`showPickerDialogRV`).
- `ScriptsBD/Sp/`: `iLSALDRVA_ForReciboItraffic`, `iLSALDRVA_ListItraffic`, `iRecibo_AfterSave`, `iAsiento_CreateRecibo`.
- `ScriptsBD/Func/fsp_SaldoReserva.sql`.
- Tablas: `recibo.Cod_agcia`, `rec_rva`, `factura.Cod_agcia`, `reserva.Cod_agcia`, `reserva.Cod_agcia2`.

## Cambios hechos
Sólo consulta; no se modificó Softur.Serenity.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Las facturas de recargo generadas por el recibo quedan en el secundario, mientras la reserva y sus recibos quedan en el principal. [código]
- `Agencia.Cod_agcia2` (ABM de clientes) es otro campo: vincula clientes en el maestro, no en la reserva. No confundirlo. `iLSALDRVA_ForReciboItraffic` lo usa al buscar facturas por comprobante; no se analizó a fondo. [código]

## Pendientes
- [ ] Definir si se pide a desarrollo que factura, recibo y saldo queden en el secundario — usuaria.

## Cómo validar
En una base de test: reserva con secundario, facturar, cargar recibo y correr Saldo cliente para el principal y para el secundario.

## Datos que pueden quedar viejos
No aplica.
