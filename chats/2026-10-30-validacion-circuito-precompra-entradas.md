# Validación en el sistema del circuito de precompra de entradas (anticipo → valor real)

- **Fecha:** 2026-10-30
- **Proyecto / cliente:** Softur — iTraffic, cliente Cuenca del Plata (circuito de Grace / Tesorería)
- **Relacionado con:** [2026-10-29-proceso-por-sector-v2-cuenca-del-plata-parte-3.md](2026-10-29-proceso-por-sector-v2-cuenca-del-plata-parte-3.md)

## Objetivo
Validar contra el código el circuito propuesto por la usuaria: día 1, autorización por el anticipo y OP con forma de pago = cuenta "Anticipo entradas"; día 2, autorización por el valor real y OP de Anticipo entradas contra banco.

## Estado final
Respondido en el chat. Conclusión: tal como está escrito, el circuito tiene los asientos invertidos. Se propuso el orden correcto.

## Cómo funciona en el sistema
- La autorización no genera asiento: se contabiliza cuando una OP la aplica (`iAutorizacion_Contabiliz` sólo marca "Contabilizó"). `[código]`
- En la OP, la línea **Debe** de una autorización usa la **Cuenta** de la autorización (`Autoriza.Cta_anti`, que se completa con la cuenta anticipo del operador, o `Nro_cuen2` con `AT_OPENROCUEN2`); si está vacía, la cuenta del operador. El saldo sale de `fsp_SaldoAutorizacionvspago`. `[código]`
- Con la config `HABERAUTOMATICOXAUTORIZA`, la OP arma sola la línea **Haber** con la "Cuenta Contable" de la autorización (campos Forma Pago + Cuenta Contable). `[código]`
- La OP también puede imputar el saldo de una OP anterior (opción "orden de pago / devolución", `tipocc` 7, `Idordenpagimp`); existe la reimputación de OP (`ReimputarOp`). `[código]`

## Problemas del circuito tal como está escrito
1. La autorización por el valor real nunca la aplica una OP: queda con saldo pendiente y aparece de nuevo para pagar (riesgo de doble pago). La del anticipo queda "pagada" sin estar imputada al planning. `[código]`
2. El banco sale el día 2, pero la plata sale el día 1 (precompra): la conciliación bancaria queda desfasada un día. `[hipótesis]`
3. Si el real difiere del anticipo, la diferencia queda en Anticipo entradas o en la cuenta del operador, sin regla que la cierre. `[hipótesis]`

## Circuito propuesto
- **Día 1:** autorización de anticipo por el estimado, con Cuenta (Debe) = Anticipo entradas y Forma de pago/Cuenta contable = Banco → OP: Debe Anticipo entradas / Haber Banco.
- **Día 2:** autorización por el real, imputada al planning, con Cuenta = cuenta del operador y Forma de pago = Anticipo entradas → OP: Debe operador / Haber Anticipo entradas. Si el real es mayor, la diferencia va con una segunda línea Haber Banco; si es menor, el saldo queda en Anticipo entradas para el día siguiente.
- Validarlo en la base de Cuenca: si `HABERAUTOMATICOXAUTORIZA` está activa, si "Cuenta" es editable en la autorización y la cuenta anticipo del operador de entradas. `[hipótesis]`

## Archivos, tablas y objetos relevantes (Softur.Serenity)
- `Softur.Serene.Web/Modules/G_Proveedores/Autoriza/AutorizaForm.generated.cs`, `AutorizaDialog.ts` (`updateOpe`: Cta_anti ← Cta_anticipo)
- `Softur.Serene.Web/Modules/G_Proveedores/Ordenpag/OrdenpagForm.generated.cs`
- `Softur.Serene.Web/Modules/G_Proveedores/Mov_ord/Mov_ordOPEditor.ts` (picker de saldos, `HABERAUTOMATICOXAUTORIZA`)
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/iLSALDPROV_ForOPA_FPP_Itraffic.sql` (`tipocc` 6 autorizaciones, 7 OP)
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/iAutorizacion_Contabiliz.sql`
- Tablas: `Autoriza` (`Cta_anti`, `FormaPago`, `CuentaContable`), `Imputaci`, `Ordenpag`, `Mov_ord`, `Operador` (`Cta_anticipo`, `Nro_cuenta`)

## Pendientes
- [ ] Confirmar con Cuenca la config `HABERAUTOMATICOXAUTORIZA` y la cuenta Anticipo entradas; actualizar el documento "Proceso por sector v2" si se adopta el circuito corregido — usuaria.
