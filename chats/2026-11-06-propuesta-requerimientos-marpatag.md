# Propuesta de requerimientos para Marpatag (descriptivo + costos y plazos)

- **Fecha:** 2026-11-06
- **Proyecto / cliente:** Softur — iTraffic, cliente Marpatag
- **Actualiza a:** [2026-11-04-tabla-requerimientos-precios.md](2026-11-04-tabla-requerimientos-precios.md) (la tabla era de Marpatag)

## Objetivo
Armar con marca Softur el documento que explica los seis requerimientos pendientes de Marpatag y, en otra página, el plazo y el costo de cada uno.

## Estado final
Terminado (5 páginas), sin capturas de pantalla. `Trabajo/Entregables/Propuesta de requerimientos - Marpatag (marca Softur).docx` y `.pdf`.

## Decisiones y por qué
- Requerimientos, plazos y precios (dados por la usuaria): `[decisión]`
  - 357537 Voucher en inglés (Voucher V2 y Voucher Spirit V2; las traducciones de los textos fijos ya fueron solicitadas) — 20 días — USD 350.
  - 358086 Importador de pasajeros por file (planilla con todos los pasajeros de una reserva) — 20 días — USD 250.
  - 358619 Liquidaciones adjuntas a facturas (el correo de la factura suma el PDF de la liquidación de la reserva; una por reserva si la factura es múltiple) — 30 a 40 días — USD 420.
  - 357919 Nuevo reporte en Factura de Compra List con la cuenta imputada a cada concepto (varias imputaciones = varias líneas) — 30 a 40 días — USD 500.
  - Sin número: Reporte de cupos en Ficha Operativa (filtro por período; servicios con cupo disponible y consumido y códigos de reserva) — 30 a 40 días — USD 500.
  - 358356 Alerta de poca disponibilidad al cargar un servicio en la reserva — 40 a 50 días — mejora sin costo.
  - Total USD 2.020 (357537 en USD, se confirma la hipótesis de la tabla).
- Estructura: portada con datos y tabla de requerimientos; secciones 01–06 con "Hoy" / "Qué proponemos"; 07 "Costos y plazos" en página aparte. `[decisión]`
- Supuestos propios, a validar por la usuaria: `[hipótesis]`
  - "Valores en USD, más IVA" (como en PaxDirect) y "plazos desde la aprobación de la propuesta".
  - El voucher en inglés se elige al emitir desde la reserva.
  - Columnas de ejemplo de la planilla de pasajeros; informe de importados y filas con error.
  - La alerta no bloquea la carga y el umbral de "poca disponibilidad" se define con Marpatag.
  - El reporte de factura de compra respeta los filtros del listado.

## Archivos, tablas y objetos relevantes
- Softur.Serenity (sólo lectura, `git pull` previo): `[código]`
  - Vouchers: `Softur.Serene.Web/Modules/Reports/Templates/Clavis_Marpatag/VOUCHER_RVA2_SPIRIT.html`; `VOUCHER_RVA2` en `getReportDataReserva`.
  - Pasajeros: `ScriptsBD/Sp/IImport_Pasajero.sql`, `IImport_PasajeroGrupo.sql`, `Sp_Configs/PlantillaImport_PasajeroGrupo.sql` (importadores existentes al maestro/grupo, no por reserva); módulo `N_Varios/Import*`.
  - Correo de factura: `ScriptsBD/Sp/MailCreateFactura.sql` (adjunta el PDF de la factura; configs `CREAMAILFACTURA`, `SENDMAILXCAMPO`, `MAILFACTURAXTIPORVA`, `ENVIAMAILNC`).
  - Factura de compra: `Softur.Serene.Model/Modules/Z_Reportes/FacturaCompra_List/Entities/FacturaCompra_List.cs` (tiene `nro_cuenta` / `nombrecuent`).
  - Cupos: `E_Ventas/Det_rva/Det_rvaEditorDialog.ts` `getCupoEstado()` → `C_Cupos.DetRvaCupoService.GetCupoItem` (config `IT_ITEMESTADOCUPO`, bloqueo con `IT_BLOCKITEMSINCUPO`); Ficha Operativa en `J_Receptivo/FichaOperativa`; cupos en `Modules/C_Cupos` (`Bloserv`, etc.).
- Plantilla: paquete de `Minuta de reunion - Oportunidades con la migracion a iTraffic (marca Softur).docx`.
- Generador: script PowerShell en el scratchpad de la sesión (no persistente).

## Cambios hechos
- Se creó el .docx y el .pdf en Entregables. Nada modificado en Softur.Serenity.

## Errores y cómo se resolvieron
- En PowerShell, una función llamada `R` no se ejecuta: el alias `r` (Invoke-History) tiene prioridad sobre las funciones. Usar nombres que no choquen con alias (`R`, `P`, `C`, `H`...).
- No hay Python ni Node en la PC; el .docx se arma con PowerShell + `System.IO.Compression.ZipFile` y se exporta a PDF por COM de Word.

## Riesgos
- Las condiciones (más IVA, plazo desde la aprobación) y los detalles funcionales supuestos pueden no coincidir con lo acordado. `[hipótesis]`

## Pendientes
- [ ] Validar condiciones y supuestos; decidir si se suman capturas (Caracol test) — usuaria.
- [ ] Enviar la propuesta a Marpatag — usuaria.
- [ ] Número de requerimiento del reporte de cupos — usuaria.

## Cómo validar
Abrir el PDF: 5 páginas; portada con tabla de 6 requerimientos; secciones 01–06; página 5 con la tabla de costos (total USD 2.020) y condiciones.

## Datos que pueden quedar viejos
- Precios y plazos de los seis requerimientos — (foto al 2026-11-06)
