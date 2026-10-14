# Reporte con formato de asientos para la reserva de prueba (Caracol)

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — ambiente de testeo (base iTraffic Caracol)
- **Actualiza a:** [2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-8.md](2026-10-13-asiento-liq-rlq-manual-reserva-cambio-de-precio-parte-8.md)

## Objetivo
Generar una vista de los tres asientos cargados por la usuaria (previsión, reversión y previsión actualizada) con el mismo formato visual que el asiento de ejemplo.

## Estado final
Parcial. Se generó el HTML con los datos propuestos en el chat; no se pudo contrastar contra lo realmente cargado porque la sesión del navegador de Claude había vencido.

## Decisiones y por qué
- Formato: una tarjeta por asiento con encabezado (id, fecha, comprobante, moneda, TC) y tabla Cuenta / Nombre / Cliente-Operación / Comprobante / Debe / Haber / Información, con fila de total. `[decisión]`
- Los ids, números de asiento, fecha y descripciones salen de la captura de la usuaria. `[datos]`
- Las líneas y el ajuste de 100 en `4314` son los propuestos en el chat, no leídos del sistema. `[hipótesis]`

## Archivos, tablas y objetos relevantes
- `../asientos-reserva-RA3745.html` (carpeta de trabajo, fuera del repo de memoria).
- No se consultó código de Softur.Serenity.

## Cambios hechos
Se creó el HTML.

## Errores y cómo se resolvieron
- El servicio de asientos devolvió "NotLoggedIn" — sesión vencida en el navegador de Claude — pendiente de que la usuaria vuelva a iniciar sesión.

## Riesgos
El reporte puede diferir de lo cargado (cuenta del ajuste, descripciones, comprobante).

## Pendientes
- [ ] Verificar el HTML contra los asientos reales cuando haya sesión — Claude.

## Cómo validar
Comparar cada tarjeta con el asiento del mismo id en `H_Contabilidad/Asiento`.

## Datos que pueden quedar viejos
- Ids de asiento de la reserva de prueba: previsión, reversión y actualizado, consecutivos — (foto al 2026-10-13)
