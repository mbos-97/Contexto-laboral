# Autorización de pago: sólo trae las reservas en reales

**Fecha:** 2026-10-28

## Objetivo

Seguir con [requisitos de la cotización operativa](2026-10-28-autorizacion-pago-cotizacion-operativa-requisitos.md). La AUT sólo trae las reservas en moneda reales; las de otras monedas no aparecen.

## Estado final

El SP **no filtra por la moneda de la reserva**. Lo que define si un ítem aparece es si hay un camino de conversión desde la **moneda del costo del ítem** hasta la **moneda de la AUT** en las tasas de la AUT. Que aparezcan sólo las de reales indica que en las tasas de la AUT falta la conversión de las otras monedas. `[código]`

## Decisiones y por qué

No aplica.

## Archivos, tablas y objetos relevantes

- `iLSALDPROV_ForOPA_FPP_Itraffic.sql`: no hay filtros `reserva.moneda = @moneda`. Los ítems entran por `det_rva.Cod_moneda` × `@comprobcambio` con `monedadestino = @moneda`. `[código]`
- `@comprobcambio`: se arma desde `xmlcambio` (base dólar: D → X por cada fila), más X → X (1), X → D (1/c) y X → Y = (1/cX)·cY. Para convertir entre dos monedas que no son dólar, hacen falta las **dos** tasas desde el dólar. `[código]`
- `ComprobateHelper.ts`: `setPesoValue` (el campo **Cambio** de la AUT) **sólo** carga o actualiza la tasa **D → P** (pesos). Las demás monedas salen de las tasas por defecto (`iMonecoti_RecuperaxFecha`) o se cargan con el **editor de tasas (balanza)** (`processTasaEditor` → `tasasToXml`). `[código]`

## Cambios hechos

No aplica.

## Errores y cómo se resolvieron

No aplica.

## Riesgos

- Una AUT en dólares con ítems costeados en dólares necesita una fila D → D en las tasas; no se verificó que siempre venga en las tasas por defecto. `[hipótesis]`

## Pendientes

- Confirmar la moneda de la AUT, la moneda del costo de las reservas que no aparecen y lo que muestra la balanza.

## Cómo validar

En la AUT, abrir la balanza y comprobar que estén las filas Dólar → (moneda de la AUT) y Dólar → (moneda del costo de cada reserva), con cambio distinto de 0. Después agregar la reserva.

## Datos que pueden quedar viejos

Código al 2026-10-28.
