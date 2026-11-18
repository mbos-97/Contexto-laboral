# Manual de uso de iConnect Marpatag — sección 08 con listado y detalle de reservas

- **Fecha:** 2026-11-13
- **Proyecto / cliente:** Marpatag — iConnect (venta web B2B sobre iTraffic)
- **Actualiza a:** [2026-11-13-manual-uso-iconnect-marpatag.md](2026-11-13-manual-uso-iconnect-marpatag.md)

## Objetivo
Completar en el manual el Panel de reservas con datos reales, buscando desde Mi panel con el usuario TEST (lo pidió la usuaria).

## Estado final
Hecho. Manual regenerado: `Entregables/Manual de uso iConnect - Venta web B2B - Marpatag (marca Softur).docx` + PDF, 25 páginas. La sección 08 suma 5 capturas (listado, encabezado, datos y documentos, pasajeros y servicios, totales y datos de pago). En las capturas se ocultaron los datos del pasajero, el nombre del vendedor y los datos bancarios. `[decisión]`

## Qué se relevó (pantallas)
- Panel de reservas (`/bookings`): tipo de fecha (Realizada = `C`, Salida = `S`) + rango. Del 01/05 al 13/11/2026, el usuario TEST tenía 78 reservas (2 ACTIVA, 76 CXL). Filtros: código y estado. Tarjeta: fecha de creación, pasajero, número de reserva (prefijo `OB`), total a pagar agencia. Diez reservas por página. `[datos]`
- Detalle (`/booking`): botones Salir presupuesto, **Volver a cargar reserva** (enlaza al inicio; no se probó) y Volver. Muestra fecha de creación, referencia, número, total a pagar agencia, origen (agencia), vendedor, creador, IN/OUT, **número de backoffice** (file de iTraffic), los botones **Liquidación** (PDF `pdfreportgenerator/.../RES1/pdf/f{file}`) y **Estado de cuenta** (PDF `htmlreportgenerator/.../FSALDRVA/pdf/{file}`), pasajeros (tipo, nombre, fecha de nacimiento, documento), servicios (fechas y estado, ej. DC), el desglose "El total a pagar incluye" y los datos para depósito/transferencia con el correo para el comprobante. `[datos]`
- En la reserva vista, el desglose cierra: (bruto − comisión) + IVA 10,5% = total neto. En el carrito de la parte 1 no cerraba. `[datos]`

## Archivos, tablas y objetos relevantes
- iConnect Marpatag: `/bookings`, `/booking`. Informes `RES1` (plantillas `Softur.Serene.Web/Modules/Reports/Templates/RES1_*.cshtml` en Softur.Serenity) y `FSALDRVA` (no ubicado en este relevamiento).

## Cambios hechos
Ninguno en el sistema (sólo búsquedas y lectura).

## Errores y cómo se resolvieron
- El rango de fechas se carga con un calendario doble (daterangepicker): se navega con las flechas y se hace clic en el día de inicio y en el de fin.

## Riesgos
El detalle de la reserva expone datos personales del pasajero y la cuenta bancaria de Marpatag: en cualquier captura para documentos, ocultarlos. `[decisión]`

## Pendientes
- [ ] Confirmar el significado de los estados del servicio (ej. DC) y qué hace "Volver a cargar reserva" — usuaria.

## Cómo validar
Mi panel › Ver todas las reservas › Fecha de Realizada, del 01/05/2026 al 13/11/2026 › Buscar reserva › filtrar ACTIVA.

## Datos que pueden quedar viejos
- Cantidad de reservas del usuario TEST (78 al 13/11/2026).
