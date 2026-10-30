# Saldo cliente: ver pendientes por moneda (USD y $ por separado)

**Fecha:** 2026-10-28

## Objetivo

Encontrar en Softur.Serenity un reporte de Saldo cliente que deje ver, para un cliente, todo lo pendiente en USD y todo lo pendiente en $, cada uno en su moneda.

## Estado final

Se puede con el listado estándar **Saldo cliente** (`Z_Reportes/SaldoCliente_List`) usando dos filtros de moneda, y se corre una vez por moneda. No hay un informe que muestre las dos monedas juntas sin convertir. `[código]`

## Decisiones y por qué

No aplica (consulta).

## Archivos, tablas y objetos relevantes

- Pantalla: `Softur.Serene.Web/Modules/Z_Reportes/SaldoCliente_List/` (`SaldoCliente_ListGrid.ts`, `SaldoCliente_ListColumns.cs`, `SaldoCliente_ListRequest.cs`). SP: `Migrations/DefaultDB/ScriptsBD/Sp/iLSALDRVA_ListItraffic.sql`. `[código]`
- Filtro **`MonedaRva`** (texto "Moneda Reserva", default "Moneda Filtro"): deja sólo las reservas con `reserva.moneda` igual a la elegida y los recibos sin reserva de esa moneda (`recibo.moneda`). `[código]`
- Filtro **`MonedaSaldo`** (parámetro `@monedalistado`, default "Moneda 1"): convierte todos los importes a esa moneda con `fsp_TraeCambioComprob`. Si queda vacío usa `P` ($), salvo que se filtre una sola reserva (toma la moneda de esa reserva). `[código]`
- Informe `SALDOCLIENTE_USD` fuerza `@monedalistado = 'D'`: convierte todo a USD; no separa. `[código]`
- Plantillas `Reports/Templates/SALDOCLIENTE*.cshtml`: agrupan por reserva; ninguna separa ni subtotaliza por moneda. Botones de la grilla: agrupar por cliente, por reserva o sin grupo. `[código]`
- Textos de default por cliente: `Db.SaldoCliente_List.MonedaRva.DefaultValue` / `Db.SaldoCliente_List.MonedaSaldo.DefaultValue`. `[código]`

## Cambios hechos

No aplica (sólo lectura).

## Errores y cómo se resolvieron

No aplica.

## Riesgos

- El filtro es por **moneda de la reserva**, no por moneda de cada servicio. Si una reserva mezcla servicios en distintas monedas, todo su saldo queda en la moneda de la reserva. `[código]`
- Si se filtra la moneda de la reserva pero no la moneda del listado, los saldos USD salen convertidos a $ al cambio. `[código]`

## Pendientes

- Si un cliente quiere ver las dos monedas en un solo informe: desarrollar una plantilla o un botón "Agrupar por moneda" con importes en la moneda original. Hoy el SP convierte todo a una sola moneda, así que agrupar la grilla no alcanza. `[hipótesis]`

## Cómo validar

Saldo cliente → Cliente X, Moneda Reserva = USD, Moneda = USD → saldo pendiente en USD. Repetir con $ / $. La suma de las dos corridas = todo lo pendiente del cliente. `[hipótesis]` (no probado en un sistema)

## Datos que pueden quedar viejos

Código al 2026-10-28.
