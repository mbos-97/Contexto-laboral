# Autorización de pago en otra moneda (parte 2): el Cambio está cargado y el ítem no aparece

**Fecha:** 2026-10-28

## Objetivo

Seguir con [parte 1](2026-10-28-autorizacion-pago-otra-moneda.md): con el Cambio cargado en la autorización, la reserva igual no aparece para imputar.

## Estado final

Se listaron las condiciones del SP para que un ítem aparezca y una consulta de diagnóstico. Sin acceso a la base del cliente. `[código]`

## Decisiones y por qué

No aplica.

## Archivos, tablas y objetos relevantes

SP `iLSALDPROV_ForOPA_FPP_Itraffic.sql`, rama `@tipocc = 3` (líneas ~1211-1430), y función `fsp_SaldoReservavsAutorizacion` `[código]`:
- **Operador:** sólo trae ítems con `det_rva.cod_oper` = operador de la autorización.
- **Saldo:** `fsp_SaldoReservavsAutorizacion` = Σ(`costol` + `ivacostol`) de los ítems de ese operador **en la moneda del costo del ítem** − lo ya autorizado **en esa misma moneda**, × cambio. Si el costo es 0, el saldo es 0.
- **Ocultan saldos chicos o en 0:** `LFILTRASALDOPROV = .T.` (saldo ≤ `TOLERANCIASALDOAUTFPP`, default 0,50) y `NOIMPUTASALDOMENORACERO = .T.` (saldo ≤ 0).
- **Cotización:** `@comprobcambio` se arma desde el XML del Cambio / tasas de la autorización, con base dólar y combinaciones derivadas. Si el costo del ítem está en una tercera moneda sin tasa cargada, con planning no aparece (el join exige `d2.Cod_moneda = cbio.moneda`).
- **Planning:** con `CCPCONPLANNING = .T.` o con `?idplanning` en el campo reserva, usa `fsp_SaldoPlanningvsComprob` y exige que el ítem esté en ese planning.
- **Fechas:** `fec_sal` y `fec_vence` de la reserva tienen que caer en los rangos del filtro (por defecto, todos).

## Cambios hechos

No aplica.

## Errores y cómo se resolvieron

No aplica.

## Riesgos

- Si la reserva se guardó después de cambiarle la moneda y recostear, el costo quedó en 0 y la reserva no va a aparecer hasta corregir los costos. `[hipótesis]`

## Pendientes

- Resultado de la consulta de diagnóstico del cliente.

## Cómo validar

```sql
select r.rva, r.moneda, d.cod_oper, d.cod_moneda, d.costol, d.ivacostol from reserva r join det_rva d on d.idreserva = r.idreserva where r.rva = '<RVA>'
select Variable, Valor from Config where Variable in ('LFILTRASALDOPROV','NOIMPUTASALDOMENORACERO','TOLERANCIASALDOAUTFPP','CCPCONPLANNING','IT_CHANGEMONEDARVA')
```

## Datos que pueden quedar viejos

Código al 2026-10-28.
