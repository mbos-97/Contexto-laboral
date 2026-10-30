# Nombre grupo (Surface): cómo está hecho y qué falta para Autorización de pago

**Fecha:** 2026-10-28

## Objetivo

Relevar en Softur.Serenity el desarrollo del campo "Nombre grupo" (config + traducciones de visibilidad en recibo, reserva, presupuesto, orden de pago y factura de venta) y saber si se puede mostrar también en Autorización de pago sin tocar código.

## Estado final

Respondido: **no se puede sólo con configuración/traducción; requiere desarrollo.** La tabla, la entidad y el formulario de Autorización de pago (`Autoriza`) no tienen el campo. `[código]`

## Decisiones y por qué

- Ninguna decisión comercial todavía. Queda como pedido a desarrollo si el cliente lo necesita.

## Archivos, tablas y objetos relevantes

Cómo funciona hoy `[código]`:
- **Visibilidad por traducción:** atributo `VisibleFromTraduction` (`Softur.Serene.Web/Modules/Common/VisibleFromTraductionAttribute.cs`) busca el texto `Db.<Entidad>.<Campo>.Visible`; si vale `true`/`false` manda, si está vacío usa el default del atributo (en estos forms, `false` = oculto). Lo mismo `RequiredFromTraduction` con `.Required`.
- Claves en `App_Data/texts/user.texts.invariant.json`: `Db.Recibo.Nombregrupo.Visible`, `Db.Ordenpag.Nombregrupo.Visible`, `Db.Presupu.Nombregrupo.Visible`, `Db.Fac_prov.Nombregrupo.Visible`, `Db.FcaturacionWizard.Nombregrupo.Visible/Required`, `Db.Factura.Nombregrupo.Required`, `Db.Reserva.Nombregrupo.Required`; títulos "Grupo" para Recibo, Fac_prov y Ordenpag. Son traducciones editables por cliente (pantalla de traducciones).
- **Config `NOM_GROUP_SURFACE`** (tabla `Config`, `.T.`): autocompleta el grupo desde la reserva (`Reserva.Productos`, lookup `Parame` código `TPRO`) en `ReciboDialog.ts`, `OrdenpagDialog.ts` (desde la reserva del detalle o desde la factura de proveedor), `FacturaDialog.ts` (además muestra/oculta el campo), `Fac_provDialog.ts`, `FacturacionWizard.ts`, `FacturacionElectPorLotesService`, y SP `iLSALDPRO_ListItraffic`.
- Config relacionada `LTRAENOMGRUPO` (SP `iLSALDRVA_ListItraffic`, saldo de clientes) y `getReportDataFactura.sql` (nombre de grupo en pasajero por config, commit del 2026-10-27).
- Campo en forms: `ReciboForm`, `OrdenpagForm`, `FacturaForm` (`[VisibleFromTraduction(false), RequiredFromTraduction(false)]` + `LookupEditor ParameTable TPRO`), `PresupuForm` (categoría "Mas Datos"), `ReservaForm`.
- Columnas: `Recibo.Nombregrupo` varchar(20), `Ordenpag.NombreGrupo` varchar(50), `Factura`, `Fac_prov`, `Presupu`, `Reserva` (scripts en `Migrations/DefaultDB/ScriptsBD/Tables/`).
- **Autorización de pago:** `Autoriza` (tabla `ScriptsBD/Tables/Autoriza.sql`, `AutorizaRow`, `AutorizaForm.generated.cs`, `AutorizaDialog.ts`, módulo `G_Proveedores/Autoriza`): sin columna ni propiedad `Nombregrupo`. Su detalle es `Imputaci`. `[código]`
- Commits de referencia: `38bf88bc9c` (LTRAENOMGRUPO), `6b48b0ff0a` (presupuesto), `9ed0e65c13` / `ccbfa31cad` (factura y wizard), `24c40f0a9e` ("Producto" → "Nombre grupo" en listados).

## Cambios hechos

No aplica (sólo lectura).

## Errores y cómo se resolvieron

No aplica.

## Riesgos

- En Recibo la columna es varchar(20) y en otras 50: un grupo largo podría truncarse. `[código]`
- El "nombre grupo" de Surface en la reserva sale de `Productos` (TPRO), no de `Reserva.Nombregrupo`. `[código]`

## Pendientes

- Si un cliente lo pide: desarrollo para Autorización de pago (ver "Cómo validar" / respuesta: columna + Row + Form con `VisibleFromTraduction(false)` + texto `Db.Autoriza.Nombregrupo.Visible` + autocompletado opcional con `NOM_GROUP_SURFACE` en `AutorizaDialog.ts` + reportes de la autorización si se quiere impreso).

## Cómo validar

Con `NOM_GROUP_SURFACE = .T.` y `Db.Ordenpag.Nombregrupo.Visible = true`, abrir una OP con reserva en el detalle: el campo aparece y se completa. En Autoriza no hay campo hasta que se desarrolle.

## Datos que pueden quedar viejos

Estado del código al 2026-10-28 (rama traída con `git pull` ese día).
