# Facturas de Ventas: tipo de subdiario y factura multi-reserva

- **Fecha:** 2026-11-18
- **Proyecto / cliente:** Softur (consulta general)
- **Actualiza a:** [2026-11-18-reporte-reservas-en-factura-multi-reserva.md](2026-11-18-reporte-reservas-en-factura-multi-reserva.md)

## Objetivo
Confirmar si en Reportes › Facturas de Ventas, con Tipo Subdiario "Agrupa x Nro Factura", una factura multi-reserva aparece con una fila por reserva.

## Estado final
Terminado. Con "Agrupa x Nro Factura" no se ve cada reserva; hay que usar "Agrupa x reserva".

## Decisiones y por qué
- Corrige la memoria anterior: el listado no siempre trae una fila por reserva; depende del Tipo Subdiario (`Parame` código `LSVT`). [código]
- **Agrupa x Nro Factura** (`@tiposubdiario = 1`, también el valor por defecto si llega nulo): `iLFACTCLI_ListItraffic` agrupa por tipo_comp, tipo_fact, nro_fact, sucursal, iva_con, fec_fact, comprob_cod_comp y dev_iva, y muestra `min(rva)`. La factura multi-reserva sale como **una sola fila** con el total sumado y sólo la reserva de número más bajo. [código]
- **Agrupa x reserva** (`@tiposubdiario = 2`): sin GROUP BY, una fila por registro de factura con su `rva`. La factura multi-reserva sale como varias filas con el mismo número, una por reserva. [código]

## Archivos, tablas y objetos relevantes
- Softur.Serenity: `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/iLFACTCLI_ListItraffic.sql` (ramas `@tiposubdiario = 1` y `= 2`); `ScriptsBD/DataDefault/ParameDefault.sql` (`LSVT`: 1 Agrupa x Nro Factura, 2 Agrupa x reserva); `Softur.Serene.Web/Modules/Common/StoreProcedureKeys.cs` (`FacturaVenta = "iLFACTCLI_ListItraffic"`).

## Cambios hechos
No aplica.

## Errores y cómo se resolvieron
- La memoria anterior decía que el listado traía una fila por reserva — no se había mirado el tipo de subdiario — se aclara que sólo pasa con "Agrupa x reserva".

## Riesgos
- Con "Agrupa x Nro Factura" la columna rva puede hacer pensar que la factura es de una sola reserva.

## Pendientes
No aplica.

## Cómo validar
- Reportes › Facturas de Ventas, mismo rango de fechas: con "Agrupa x Nro Factura" la factura multi-reserva tiene que salir en una fila; con "Agrupa x reserva", una fila por reserva con el mismo nro_fact.

## Datos que pueden quedar viejos
No aplica.
