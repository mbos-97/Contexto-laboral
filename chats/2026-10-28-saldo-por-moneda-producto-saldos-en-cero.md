# "Saldo por moneda producto" sale con saldos en 0

**Fecha:** 2026-10-28

## Objetivo

Ver por qué el informe `LSALDOMONE` salió con todos los saldos en 0, con estos filtros: Cliente = CONSUMIDOR FINAL, TipoSaldo = TODAS, Fecha Viaje 01/10/2026–28/10/2026, Moneda 1 y Moneda Filtro vacías, Origen cuentas a cobrar vacío.

## Estado final

Diagnóstico desde el código, sin acceso a la base del cliente. Según el SP no falta ningún filtro obligatorio. Las causas probables y cómo verificarlas están en "Cómo validar". `[código]`

## Decisiones y por qué

No aplica.

## Archivos, tablas y objetos relevantes

- `iLSALDRVA_ListItraffic.sql`: con `LSALDOMONE` el SP fuerza `@tipocc = 20`, así que el filtro "Origen cuentas a cobrar" no influye. Las columnas por moneda (`Total_/Cobro_/Saldo_Dolares/Pesos/Mep`) sólo se calculan dentro de `if @tipocc=20` (línea ~6546). `[código]`
- Hay tres caminos según la config `[código]`:
  - **Sin `REGISTROFACDIFMONEDAS = SI`** (`@SaldoMoneda = 21`). Total = `FMONTO_MONE_rv2`: lo **facturado** de reservas con `reserva.moneda` = D/P/M. Cobro = `fCOBRO_MONEDA_RVA_estadodecuenta`: sólo recibos con `comprobcambio` en esa moneda y `reserva.moneda` = esa moneda. Saldo = total − cobro.
  - **Con `REGISTROFACDIFMONEDAS = SI`** y sin `EXCELSE21`: total y cobro según `MonedaComprobante` de cada línea (`debitos` / `creditos`).
  - Con `SALMONRVAENMONLOCAL = .T.` el saldo no se recalcula como total − cobro.
- La plantilla `LSALDOMONE.cshtml` muestra las columnas tal cual vienen del SP.

## Cambios hechos

No aplica.

## Errores y cómo se resolvieron

- En la respuesta anterior se dijo "botón PDF / informes"; en pantalla el botón se llama **"Informe Saldo Clientes"** y tiene una flecha para elegir el informe. `[datos]` (captura de la usuaria)

## Riesgos

- Con TipoSaldo = TODAS también salen las reservas saldadas. Las de consumidor final con viaje ya hecho suelen estar pagas, así que el saldo 0 puede ser correcto. `[hipótesis]`
- Si `reserva.moneda` usa códigos distintos de D / P / M, el camino 21 da 0 en todo. `[hipótesis]`

## Pendientes

- Que la usuaria revise la columna `saldo` en la grilla, pruebe con TipoSaldo = CON SALDO y consulte el valor de `REGISTROFACDIFMONEDAS`, `EXCELSE21` y `SALMONRVAENMONLOCAL` en `Config`. `[hipótesis]`

## Cómo validar

1. En la grilla, mirar la columna `saldo`: si también es 0, las reservas están pagas y el informe está bien.
2. Repetir con TipoSaldo = CON SALDO.
3. Fijarse si en el informe TOTAL y COBRO también están en 0 (no se calcula) o sólo SALDO (está pago).
4. `select Variable, Valor from Config where Variable in ('REGISTROFACDIFMONEDAS','EXCELSE21','SALMONRVAENMONLOCAL','COMPROBANTES_ALL')`.

## Datos que pueden quedar viejos

Código al 2026-10-28.
