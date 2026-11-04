# Cliente secundario en la reserva: cómo funciona

- **Fecha:** 2026-11-04
- **Proyecto / cliente:** Softur / iTraffic (transversal)
- **Actualiza a:** Complementa [2026-10-09-relevamiento-marpatag-amex-dos-condiciones.md](2026-10-09-relevamiento-marpatag-amex-dos-condiciones.md)

## Objetivo
Entender cómo funciona el cliente secundario según el código de Softur.Serenity.

## Estado final
Terminado para pantalla, facturación, recibos, percepciones y listados principales. No se probó en una base ni se revisaron a fondo los informes de estadísticas, comisiones y tarifas.

## Decisiones y por qué
- Dónde se carga: campo `Cod_agcia2` de la reserva ("Cliente secundario"), solapa Más Datos, Datos Administrativos. Elige de la lista de clientes y permite crear uno. Existe también en presupuesto. [código]
- Con la config `lfacagciados = .T.`, la factura toma CUIT, razón social, dirección, condición de IVA y letra del secundario (la letra `T` se mantiene). [código]
- La factura sigue con `Cod_agcia` del cliente principal (`@cod_agciafactura = r.cod_agcia`). [código]
- Excepción: las facturas de recargo que genera el recibo (`iRecibo_AfterSave`) sí toman `Cod_agcia` del secundario. [código]
- Con `LTRAEDOCUPAX = .T.` y principal `CF`, `UCD` o `V`, los datos del pasajero pisan CUIT, nombre y dirección del secundario; la letra ya calculada queda. [código]
- `isp_FacturaValidate`: con config y secundario exige CUIT, tipo de documento y condición de IVA del secundario, y controla el tipo de documento contra la letra. [código]
- Factura electrónica (`FacturaElec_FromVenta`): `DocTipo` del secundario y `DocNro` de `factura.cuitfac`. [código]
- Percepciones RG 4815 y 5672: tipo y número de documento del secundario. [código]
- Listado de facturas (`iLFACTCLI_ListItraffic`): une con el secundario cuando existe, sin depender de la config. [código]
- Saldos: con `LCCMUESTRACLISECUNDARIO = .T.`, su nombre se muestra en la columna `NomZonaCliente`. [código]
- Ficha operativa: con `INFO1CODAGCIA2` se muestra "Cliente secundario: nombre" en `ExtraInfo1`. [código]
- La tabla `AgenciaSecundaria` se crea pero ningún otro código la usa: cualquier cliente puede ser secundario de cualquier reserva. [código]
- Marpatag: la idea de 2026-10-09 de usar a Amex como secundario "para estadísticas" chocaría con esto si la instalación tiene `lfacagciados = .T.`: la factura saldría con los datos de Amex. [hipótesis]

## Archivos, tablas y objetos relevantes
Softur.Serenity, commit `7fed35bc6c`:
- `Softur.Serene.Web/Modules/E_Ventas/Reserva/`: `ReservaForm.generated.cs`, `ReservaDialog.ts`, `ReservaColumns.generated.cs`.
- `Softur.Serene.Model/Modules/E_Ventas/Entities/`: `ReservaRow.generated.cs`, `PresupuRow.generated.cs`.
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/`: `iReserva_FacturaCreateUpdatexIdxMoneda`, `IReserva_CreateFacturaFee`, `isp_FacturaValidate`, `FacturaElec_FromVenta`, `iRecibo_AfterSave`, `getReportDataFactura`, `i_PercepcionImpGciasRG4815_List_PER`, `i_PercepcionImpGciasRG5672_List_PER`, `iLFACTCLI_ListItraffic`, `iLSALDRVA_ListItraffic`, `FichaOperativaxMail`, `Det_RvaCacheFicha_Update`.
- `ScriptsBD/Tables/AgenciaSecundaria.sql`, `ScriptsBD/Func/fnombre_agcia2_rva.sql`, `ScriptsBD/DataDefault/ConfigDefault.sql`.
- Tablas: `reserva.Cod_agcia2`, `presupu.Cod_agcia2`, `agencia`, `factura`, `config`.
- Manual indexado: `App_Data/AIAssistant/Manuals/Indexed/manuals_index.json` (págs. 189-190).

## Cambios hechos
Sólo consulta; no se modificó Softur.Serenity.

## Errores y cómo se resolvieron
- La búsqueda con Grep sobre todo el repo se corta por tiempo — el repo es muy grande — usar `git grep`.

## Riesgos
- Posible error en `isp_FacturaValidate` (línea 931): `tipodoc='86' or tipodoc='96' and tipo_fact='A'` rechaza un secundario con tipo de documento 86 también en factura B, porque el `and` se evalúa antes que el `or`. Sin probar. [hipótesis]
- Las facturas de recargo quedan con otro `Cod_agcia` que las facturas normales de la misma reserva. [código]

## Pendientes
- [ ] Confirmar con desarrollo la condición de la línea 931 de `isp_FacturaValidate` — usuaria.

## Cómo validar
En una base de test con `lfacagciados = .T.`: cargar secundario en una reserva, facturar y comparar los datos fiscales de la factura con el cliente de la cuenta corriente.

## Datos que pueden quedar viejos
- `lfacagciados` en `ConfigDefault.sql` — `.T.`; cada instalación puede tener otro valor — (foto al 2026-11-04)
