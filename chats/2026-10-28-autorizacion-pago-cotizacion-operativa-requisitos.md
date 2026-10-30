# Autorización de pago: qué tiene que tener la cotización operativa para que la AUT la tome

**Fecha:** 2026-10-28

## Objetivo

Seguir con [cambio operativo vs administrativo](2026-10-28-autorizacion-pago-cambio-operativo-vs-administrativo.md). El cliente **no** tiene `IT_USEMONECOTIADMIN`, así que la AUT usa la cotización operativa (`Monecoti`), y la reserva sigue sin aparecer.

## Estado final

Se detallaron los requisitos del SP `iMonecoti_RecuperaxFecha` para que una moneda tenga tasa en la AUT, más un checklist. Sin acceso a la base del cliente. `[código]`

## Decisiones y por qué

No aplica.

## Archivos, tablas y objetos relevantes

- `ComprobateHelper.ts`: pide las tasas con `Moneda = 'D'` (salvo `LCAMBIORECIBOXMONEDA = .T.`, que manda la moneda del comprobante). `[código]`
- SP `iMonecoti_RecuperaxFecha.sql`, rama operativa: para cada moneda X devuelve `Monecoti.Cambio` con **`Cod_moneda = 'D'`** y **`Monedarva = X`**, la última con `Fecha <= fecha` de la AUT. Sólo incluye monedas que estén en **`Parame` código `MONE`** y en la tabla **`Monedas`**. Una cotización cargada al revés (X → D) no se toma. `[código]`
- Con esas tasas el SP `iLSALDPROV_ForOPA_FPP_Itraffic` arma `@comprobcambio` (base dólar + combinaciones). Si la moneda de la AUT o la del costo del ítem no tiene fila, el ítem no aparece. `[código]`

## Cambios hechos

No aplica.

## Errores y cómo se resolvieron

No aplica.

## Riesgos

No aplica.

## Pendientes

- Resultado de las consultas en el cliente.

## Cómo validar

```sql
select top 5 Fecha, Cod_moneda, Monedarva, Cambio from Monecoti where Cod_moneda='D' order by Fecha desc
select Retorno, Descrip from Parame where Codigo='MONE'
select Codigo from Monedas
```

## Datos que pueden quedar viejos

Código al 2026-10-28.
