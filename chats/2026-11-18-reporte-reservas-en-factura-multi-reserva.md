# Reporte de reservas incluidas en una factura multi-reserva

- **Fecha:** 2026-11-18
- **Proyecto / cliente:** Softur (consulta general)
- **Actualiza a:** No aplica

## Objetivo
Saber si existe en el sistema un reporte o pantalla que muestre qué reservas se facturaron juntas en una factura multi-reserva.

## Estado final
Terminado. Hay dos maneras de verlo: el filtro "Multiples" de Clientes › Facturas y el listado de facturas de venta. No existe un reporte dedicado con el detalle "factura → reservas".

## Decisiones y por qué
- Una factura multi-reserva se guarda como **un registro `Factura` por reserva**, todos con el mismo `idenviomultiple`. Al emitir, `iFactura_UpdateFromCachefiscal` les pone a todos el mismo `nro_fact`, sucursal y CAE (`where idenviomultiple=@idenviomultiple`) y genera detalle y asiento por cada uno. [código]
- **Clientes › Facturas** (`FacturaIndex` → `FacturaFromWizardGrid`, columnas `FacturaFromWizardColumns`): columna/filtro rápido **"Multiples"** (`Idenviomultiple`, `LookupFiltering(RvaMultipleLookup)`). Se elige una reserva y la grilla trae todas las facturas de ese envío múltiple, cada una con su columna Rva, Total y Pasajero. El filtro llega a `isp_FacturacionTop100` como `@idenviomultiple`. Se puede exportar. [código]
- Limitación del filtro: el lookup ejecuta `iFactura_RvaMultiple` sin parámetro, que devuelve `top 50` facturas múltiples sin orden; con muchas facturas múltiples, la reserva buscada puede no aparecer en la lista. [código] El efecto en pantalla no se probó. [hipótesis]
- **Reportes › Facturas de Ventas** (`Z_Reportes/FacturaVenta_List`, SP de la familia `iLFACTCLI_ListItraffic`): trae una fila por registro de factura con columna `rva`, así que una multi-reserva aparece como varias filas con el mismo tipo y número de comprobante, una por reserva. [código]
- Config relacionada: `FacMultiPaxINOUT` (en `getReportDataFactura`) muestra pax y fechas in/out en el impreso de facturas múltiples. [código]

## Archivos, tablas y objetos relevantes
- Softur.Serenity, Web: `Modules/F_Clientes/Factura/FacturaFromWizardColumns.cs`, `RvaMultipleLookup.cs`, `FacturaFromWizardGrid.ts`, `FacturaIndex.cshtml`; `Modules/F_Clientes/FacturaWizard/FacturacionElectPorLotesService.generated.cs`; `Modules/Z_Reportes/FacturaVenta_List/*`; `Common/Navigation/NavigationItems.cs`.
- Softur.Serenity, Model: `Modules/F_Clientes/Entities/Fac_detRow.generated.cs` (Rva, Idreserva por línea); `Modules/Z_Reportes/FacturaVenta_List/Entities/FacturaVenta_List.cs`.
- SP: `iFactura_RvaMultiple`, `isp_FacturacionTop100`, `isp_FacturacionLastIdenvioMultiple`, `iFactura_UpdateFromCachefiscal`, `getReportDataFactura`, `iLFACTCLI_ListItraffic`.
- Tablas: `Factura` (`idenviomultiple`, `rva`, `idreserva`, `nro_fact`), `Fac_det` (`Rva`, `Idreserva`, `Iddet_rva`).

## Cambios hechos
No aplica.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- El filtro "Multiples" puede no listar la reserva buscada por el `top 50` del lookup.

## Pendientes
- [ ] Probar en una base el filtro "Multiples" de Clientes › Facturas; si la reserva no aparece, evaluar con desarrollo que `iFactura_RvaMultiple` ordene por lo más reciente o busque por reserva — usuaria.

## Cómo validar
- Clientes › Facturas › filtro "Multiples" › elegir una reserva de una factura multi-reserva: deben aparecer todas las reservas con el mismo número de factura.
- Reportes › Facturas de Ventas con el rango de fechas de esa factura: deben verse varias filas con el mismo número, una por reserva.

## Datos que pueden quedar viejos
- Límite del lookup de "Multiples" — top 50 — (foto al 2026-11-18)
