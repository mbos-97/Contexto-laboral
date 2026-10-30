# Autorización de pago: ¿toma el cambio operativo o el administrativo?

**Fecha:** 2026-10-28

## Objetivo

Seguir con [parte 3](2026-10-28-autorizacion-pago-otra-moneda-parte-3.md). La usuaria cargó el tipo de cambio **operativo** y pregunta si la autorización en otra moneda no trae la reserva porque usa el **administrativo**.

## Estado final

Sí, puede ser. Depende de la config `IT_USEMONECOTIADMIN`. `[código]`

## Decisiones y por qué

No aplica.

## Archivos, tablas y objetos relevantes

- `AutorizaDialog.ts` → `ComprobateHelper.ts` (`loadDefaultTasasIfNeed`, `updateMoneda`, `ShowTasasEditor`) → `Fac_provService.GetDefaultComprobCambio` → `ComprobanteRepository.getDefaultComprobcambio` → SP **`iMonecoti_RecuperaxFecha`** (`StoreProcedureKeys.CotizacionMoneda`). `[código]`
- SP `iMonecoti_RecuperaxFecha.sql` `[código]`:
  - con **`IT_USEMONECOTIADMIN = .T.`**: lee **`Monecoti_admin`** ("Cambio divisas administrativo");
  - sin esa config: lee **`Monecoti`** ("Cambio Moneda Operativo");
  - en los dos casos toma la última cotización con `Fecha <= fecha del comprobante`, por cada moneda de `Parame` `MONE`.
- Esas tasas forman el `ComprobCambio` / `xmlcambio` que recibe `iLSALDPROV_ForOPA_FPP_Itraffic`. Sin la tasa entre la moneda del costo del ítem y la de la autorización, el ítem no aparece. `[código]`
- La config `TASAAUT` cambia el comportamiento del editor de tasas en la AUT (`ComprobateHelper.ts`, línea ~78). `[código]`
- Hay otra pantalla de administración, "Tipo cambio administrativo" (`H_Contabilidad/Cotizac`), distinta de `Monecoti_admin`. No se verificó si la AUT la usa: según el SP, no. `[código]`

## Cambios hechos

No aplica.

## Errores y cómo se resolvieron

No aplica.

## Riesgos

- Una cotización con fecha posterior a la de la autorización no se toma. `[código]`
- Las tasas se cargan al abrir la AUT o al cambiar la moneda: si la cotización se cargó con la AUT abierta, hay que volver a abrirla. `[código]`

## Pendientes

- Confirmar el valor de `IT_USEMONECOTIADMIN` en el cliente.

## Cómo validar

`select Variable, Valor from Config where Variable in ('IT_USEMONECOTIADMIN','TASAAUT','LCAMBIORECIBOXMONEDA')`. Si `IT_USEMONECOTIADMIN = .T.`, cargar la cotización en "Cambio divisas administrativo" con fecha ≤ la de la AUT, abrir una AUT nueva, revisar las tasas con la balanza y agregar la reserva.

## Datos que pueden quedar viejos

Código al 2026-10-28.
