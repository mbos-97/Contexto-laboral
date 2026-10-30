# Autorización de pago en una moneda distinta de la reserva

**Fecha:** 2026-10-28

## Objetivo

Emitir una autorización de pago en una moneda distinta de la de la reserva (consulta urgente). En la autorización no aparecían los ítems para imputar, y al cambiar la moneda de la reserva todos los ítems quedaban en 0.

## Estado final

Respuesta operativa desde el código: la autorización **sí admite otra moneda** si tiene cargada la cotización entre la moneda del costo del ítem y la moneda de la autorización. No hay que cambiar la moneda de la reserva. Sin probar en el sistema del cliente. `[código]`

## Decisiones y por qué

No aplica.

## Archivos, tablas y objetos relevantes

- `G_Proveedores/Autoriza/AutorizaDialog.ts`: al cambiar Moneda se pasa al editor de imputaciones (`Imputaci.moneda`). Tiene el campo **Cambio** y el botón de tasas (ícono de balanza, "Modificar mas Tasas para este Comprobante") que arman `ComprobCambio`. `[código]`
- `Imputaci/ImputaciAutorizaEditor.ts`: los botones "agregar reserva" / "agregar factura" exigen operador y llaman al SP `iLSALDPROV_ForOPA_FPP_Itraffic` con `moneda`, `COD_OPER`, `tipocc` 3 (reservas) / 5 (facturas) y `xmlcambio`. `[código]`
- SP `iLSALDPROV_ForOPA_FPP_Itraffic.sql` (rama `@tipocc = 3`): `inner join @comprobcambio cbio on cbio.monedadestino=@moneda and d2.Cod_moneda=cbio.moneda`. Si falta la cotización entre la moneda del costo del ítem (`det_rva.Cod_moneda`) y la de la autorización, **el ítem no aparece**. Usa la moneda del costo del ítem, no la de la reserva. `[código]`
- `E_Ventas/Reserva/ReservaDialog.ts`: con la config `IT_CHANGEMONEDARVA`, cambiar la moneda pregunta "Recostar todos los items?" y llama a `recostear()` + `RecalcularReserva()`. Si no hay cotización o tarifa para la nueva moneda, los importes quedan en 0. `[código]` / `[hipótesis]` (lo de la tarifa)
- `Db.Autoriza.Moneda.DefaultValue` define la moneda inicial de la autorización. `[código]`

## Cambios hechos

No aplica.

## Errores y cómo se resolvieron

No aplica.

## Riesgos

- Si al cambiar la moneda de la reserva se confirmó "Recostar" y se **guardó**, los costos y ventas quedaron en 0: hay que restaurarlos. Si no se guardó, alcanza con cerrar sin guardar. `[código]`

## Pendientes

- Confirmar con la usuaria si la reserva quedó guardada con los ítems en 0.

## Cómo validar

Abrir la autorización → Operador → Moneda deseada → cargar el Cambio (y las tasas con la balanza si es una tercera moneda) → agregar reserva: tiene que aparecer el ítem convertido.

## Datos que pueden quedar viejos

Código al 2026-10-28.
