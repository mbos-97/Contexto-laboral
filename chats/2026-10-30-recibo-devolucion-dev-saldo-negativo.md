# Recibo de devolución (DEV) trae saldo negativo y no salda la reserva

- **Fecha:** 2026-10-30
- **Proyecto / cliente:** Softur Serenity — consulta funcional (Recibos)
- **Actualiza a:** No aplica

## Objetivo
Entender por qué, al hacer un recibo "Devolucion de Reserv" (DEV) y llamar a la reserva, el importe aparece negativo y la reserva no queda saldada.

## Estado final
Terminado (explicación dada; no se probó en una base real).

## Decisiones y por qué
- Al traer reservas, el recibo copia el saldo tal cual al importe del ítem (`Dolares = Saldo`), sin mirar el tipo de comprobante: no invierte el signo para DEV. `[código]`
- El saldo de reserva (`fsp_SaldoReserva`) = facturas (`Suma_ccc`) − facturas `Resta_ccc` − recibos con `Resta_ccc` (REC) **+ recibos con `Suma_ccc`** (DEV) + OP con `Suma_ccc`. `[código]`
- DEV tiene `Suma_ccc = 1`, `Resta_caja = 1`, `Par_cue1 = DEU` (datos iniciales). `[código]`
- Consecuencia: una reserva cobrada de más tiene saldo negativo (ej. −100). Si el DEV se graba con −100, suma −100 y el saldo pasa a −200. Hay que cargar el importe del ítem en **positivo** (100) y la forma de cobro (egreso de caja) por el mismo importe; así el saldo queda en 0. `[código]`
- La forma de cobro debe igualar el total de conceptos (validación `ValidMontos_Error`). `[código]`

## Archivos, tablas y objetos relevantes
- `Softur.Serene.Web/Modules/F_Clientes/Recibo/ReciboDialog.ts` — `addItem()` (Dolares = x.Saldo), `showPickerDialogRV`, `validateBeforeSave`.
- `Softur.Serene.Model/Migrations/DefaultDB/Scripts/DefaultDB_20190613_205900_fsp_SaldoReserva.sql` — función `fsp_SaldoReserva`.
- `Softur.Serene.Model/Migrations/DefaultDB/Scripts/20171002_160200_Datos_Iniciales.sql` — fila `Comprob` DEV.
- SP `iLSALDRVA_ForReciboItraffic` (ScriptsBD/Sp) — picker de saldos de reserva.
- Tablas: `Recibo`, `Rec_rva`, `Comprob`, `Comprobcambio`.

## Cambios hechos
No aplica (repo sólo lectura).

## Errores y cómo se resolvieron
- Saldo negativo en DEV que no salda — el ítem toma el saldo con signo y DEV suma a la cuenta corriente — cambiar el importe a positivo.

## Riesgos
- Si la base del cliente tiene el comprobante DEV configurado distinto (`Suma_ccc`/`Resta_ccc`), el comportamiento cambia: revisar Comprob en esa base. `[hipótesis]`
- Mejora posible (desarrollo): que `addItem` invierta el signo cuando el comprobante es DEV.

## Pendientes
- [ ] Confirmar con la usuaria que con importe positivo la reserva queda en 0 — usuaria.

## Cómo validar
Recibo DEV sobre la reserva con saldo −X: poner X positivo en el concepto y X en la forma de cobro, guardar y ver Saldo cliente de la reserva = 0.

## Datos que pueden quedar viejos
- Flags de DEV en datos iniciales (Suma_ccc 1, Resta_caja 1) — (foto al 2026-10-30)
