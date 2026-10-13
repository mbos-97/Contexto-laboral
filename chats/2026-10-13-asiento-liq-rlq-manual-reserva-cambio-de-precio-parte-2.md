# Asiento LIQ / RLQ manual: cuentas reales de la base de testeo Caracol

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — ambiente de testeo (base iTraffic Caracol)
- **Actualiza a:** [2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio.md](2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio.md)

## Objetivo
Reemplazar las cuentas supuestas de los tres asientos (LIQ 3.800, RLQ espejo, LIQ 3.900) por las que existen en el plan de cuentas de la base de testeo Caracol.

## Estado final
Terminado. Se entregaron los tres asientos con cuentas de Caracol. La carga manual queda a cargo de la usuaria.

## Decisiones y por qué
- El plan de cuentas de Caracol es de 4 dígitos (255 cuentas); las cuentas con formato `NNNNNNNN-NN` del asiento de ejemplo no existen ahí. `[datos]`
- Cuentas elegidas: deudor `1311 CLIENTES` (parcuent `DEU`); costo aéreo `2214 IATA TRANSITORIO`; costo operador terrestre `2121 PREVISIONES` (parcuent `FRE`); ingreso `4216 VENTA DE SERVICIOS VARIOS` (parcuent `ING`). `[datos]`
- Parámetros Cuentas de Caracol tiene muchas filas `FRE` / `FEE` / `ING` / `COM` / `IXT` que apuntan a cuentas con formato largo inexistentes en el plan; sólo son válidas `DEU 1311`, `FRE 2121`, `ING 4216` y `COM 4220`. `[datos]`
- En Caracol no existen los comprobantes `LIQ` ni `RLQ` y no hay ningún asiento de ese tipo. `[datos]`
- Los asientos en dólares de esa base usan cuentas con moneda pesos sin problema (ej. una orden de pago en USD contra `2111`). `[datos]`

## Archivos, tablas y objetos relevantes
- Pantallas consultadas (sólo lectura): `H_Contabilidad/Plan_cta`, `L_Configuraciones/Parcuent`, `H_Contabilidad/Asiento`, `H_Contabilidad/Comprob`.
- Softur.Serenity: mismos SP que la memoria anterior; no se consultó código nuevo.

## Cambios hechos
Ninguno en el sistema. Sólo esta memoria.

## Errores y cómo se resolvieron
- El navegador de Claude no abría el sitio con `navigate` — se abrió con `preview_start` pasando la URL.
- El inicio de sesión lo hizo la usuaria; Claude no ingresa contraseñas.

## Riesgos
- Como no hay comprobante `LIQ` / `RLQ` en Caracol, el asiento manual va a salir con otro tipo de comprobante y no va a verse igual que el ejemplo.
- Un asiento manual no queda vinculado a `liq_rva`. `[código]`

## Pendientes
- [ ] Cargar los tres asientos en Caracol — usuaria.

## Cómo validar
Cada asiento balancea; al final `1311` queda en 3.900 al debe, `2121` en 2.000 al haber y `4216` en 1.900 al haber.

## Datos que pueden quedar viejos
- Plan de cuentas Caracol: 255 cuentas — (foto al 2026-10-13)
- Parcuent Caracol con cuentas inexistentes en el plan — (foto al 2026-10-13)
