# Filtros para emitir "Saldo por moneda producto" (LSALDOMONE)

**Fecha:** 2026-10-28

## Objetivo

Indicar qué filtros de Saldo cliente aplicar para emitir el informe "Saldo por moneda producto" de un cliente con lo pendiente en USD y en $.

## Estado final

Receta armada desde el código (`SaldoCliente_ListGrid.ts`, `SaldoCliente_ListColumns.cs`, SP `iLSALDRVA_ListItraffic.sql`, `ParameDefault.sql`). No se probó en un sistema. `[código]`

## Decisiones y por qué

No aplica (consulta).

## Archivos, tablas y objetos relevantes

Filtros de la pantalla Saldo cliente y su efecto sobre `LSALDOMONE` `[código]`:
- **Agencia** (`cod_agcia`): el cliente. Es el único filtro que hace falta.
- **TipoSaldo** (Parame `TSDO`): T = TODAS, N = CON SALDO, S = SALDADAS, + / - = con saldo positivo o negativo, P / C = con saldo prepago o cta. cte. Se evalúa sobre el saldo neto de la reserva **convertido a la moneda del listado** (se borran las reservas con saldo absoluto ≤ tolerancia).
- **Origen cuentas a cobrar** (`tipocc`, Parame `TSPC`, default 2): **no influye**. Con `LSALDOMONE` el SP lo pisa a 20 o 21 según `REGISTROFACDIFMONEDAS`.
- **Moneda Filtro / Moneda Reserva** (`MonedaRva`): dejarla **vacía**. Si se completa, deja sólo las reservas de esa moneda y se pierde la otra columna.
- **Moneda 1** (`MonedaSaldo` / `@monedalistado`): no cambia las columnas $ / U$S / MEP (salen con `comprobcambio` de cada moneda); sólo afecta las columnas débito/crédito/saldo generales y el filtro TipoSaldo. Vacía = $.
- Fechas opcionales: Fecha Comprob, Fecha Vencimiento, Fecha Reserva, Fecha Viaje. Estado File, Sucursal, Vendedor, Grupo Tipo Rvas: opcionales.
- Defaults por traducción: `Db.SaldoCliente_List.<filtro>.DefaultValue` (el tipocc arranca en 2 si no hay traducción).
- Emisión: botón de PDF / informes de la grilla (`PdfExportHelper`) → elegir "Saldo por moneda producto" (alta en `InformesWebDefaultInsert.sql`, pantalla `SALDOCLIENTELIST`).

## Cambios hechos

No aplica (sólo lectura).

## Errores y cómo se resolvieron

No aplica.

## Riesgos

- Con TipoSaldo = CON SALDO, una reserva con saldo en USD y en $ que se compensan al convertir a una sola moneda podría quedar afuera. Si eso preocupa, usar TODAS. `[código]`

## Pendientes

- Probar la receta en un sistema con un cliente que tenga reservas en las dos monedas. `[hipótesis]`

## Cómo validar

Emitir el informe para un cliente y comparar SALDO $ y SALDO U$S con las corridas de Saldo cliente por moneda (Moneda Reserva + Moneda 1).

## Datos que pueden quedar viejos

Código al 2026-10-28.
