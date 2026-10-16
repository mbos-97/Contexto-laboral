# Comprobante de alta del Itinerario dinámico AI (IT Total para cotización y reserva) con identidad Softur

- **Fecha:** 2026-10-16
- **Proyecto / cliente:** Softur — alta de producto Itinerario dinámico AI (iTraffic); cliente sin definir
- **Actualiza a:** No aplica (mismo criterio que [2026-10-14-alta-itinerario-dinamico-it-total-con-marca-parte-3.md](2026-10-14-alta-itinerario-dinamico-it-total-con-marca-parte-3.md))

## Objetivo
Armar el comprobante de alta del itinerario `Travel.Itinerary.AI` (vista `itxcotfull`), separando lo que envía el cliente de lo que sale de iTraffic, con la marca Softur.

## Estado final
Terminado. `Trabajo/Entregables/Alta Itinerario dinamico AI - IT Total (marca Softur).docx` y su PDF (6 páginas A4).

## Decisiones y por qué
- Misma estructura y diseño que el alta del IT Total dinámico: portada, 01 lo que envía el cliente (con las capturas de referencia al inicio), 02 lo que se carga en iTraffic, 03 checklist. `[decisión]`
- Capturas nuevas tomadas del itinerario de prueba y anotadas con C# `System.Drawing`: recuadro naranja con número = envía el cliente; recuadro negro con letra = sale de iTraffic. `[decisión]`
- Cliente y código de cliente quedaron en blanco porque la usuaria no los indicó. `[decisión]`
- Este itinerario es un documento tipo cotización (no tiene barra de secciones ni banners): lo que define el cliente son sobre todo textos fijos. `[datos]`

## Qué es del cliente y qué sale del sistema
- **Envía el cliente** `[datos]` (relevado en la página de prueba):
  1. Imagen de portada (`banner2.jpg`, hoy 1140×785).
  2. Comentarios importantes.
  3. Notas de la política de cancelación ((*), (**), penalidad general, email para cancelaciones).
  4. Presentación del destino ("Why travel to…": título y texto).
  5. Frase de cierre ("End of your services with…").
  6. Términos y condiciones generales.
  7. Política de pago y cancelación.
  8. Pie (razón social, ciudad, web, email, teléfono de emergencia).
  - Además: nombre comercial, idiomas de los textos fijos, tipografía (hoy Georgia) y colores (encabezados #414042, textos #767171).
- **Sale de iTraffic** `[código]`:
  - Datos del viaje, resumen de cotización, precio por pasajero y estado de cuenta: de la cotización / reserva.
  - Tabla de cancelación: `det_rvapolclx` (fecha y monto de penalidad por servicio de la reserva) en `iDet_rvait_SelectBooking`.
  - Detalle por día: textos del servicio, idioma (`reserva.Oricont`), guía, vuelos; fotos de servicios (`IMAGENSERVICIOs`).
  - Teléfono de emergencia por servicio: `Telurg` del operador / proveedor.
  - Informes web `Cot_itxfullaliwen` (módulo `PRESUPU`, budget=1) y `Rva_itxfullaliwen` (módulo `RESERVA`, budget=0), título "IT:Total ALIWEN", URL `/Travel.Itinerary.AI/itinerary?...typeview=itxcotfull`.

## Archivos, tablas y objetos relevantes
- Softur.Serenity consultado (sólo lectura, con `git pull` previo): `[código]`
  - `Softur.Serene.Model/Migrations/DefaultDB/Scripts/DefaultDB_20200417_104800_InformesWebItinerario.sql` — alta de los informes AI (`itxcotfull`, `itxcotshort`, `itxhotel`, `itxvoucher`).
  - `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/iDet_rvait_SelectBooking.sql` — `@CancelationPolicy` (de `det_rvapolclx`), `@PaymentPolicy` (de `det_rvapayment`, sólo hoteles, con comentario de `Operpag`), idioma, guía, teléfono de emergencia.
  - `.../ScriptsBD/Func/ifsp_GetDatosDet_rvait.sql` — textos de servicios y ciudades.
- El proyecto web `Travel.Itinerary.AI` no está en Softur.Serenity; los textos fijos y estilos de la plantilla viven ahí (`Agents/default`). `[hipótesis]`

## Cambios hechos
- Se creó el .docx y el PDF en `Entregables`. No se tocó Softur.Serenity.

## Errores y cómo se resolvieron
- En PowerShell las variables no distinguen mayúsculas: `$Src` y `$src` pisaban la ruta — se renombró a `$SrcDir` / `$im`.
- Un arreglo de un solo elemento `@( @(...) )` se aplana — se usó `@(,@(...))`.
- `DrawRectangle` con tipos mezclados fallaba — se pasó todo a `[single]`.
- Con "conservar con el siguiente" en todos los párrafos, la sección 02 saltaba entera de página — se quitó en esa sección.

## Riesgos
- Los textos fijos de la demo mencionan a otra agencia ("Aliwen") y a Softur: son de la plantilla de ejemplo. `[datos]`
- `@PaymentPolicy` existe en el SP, pero en la demo la política de pago se ve como texto fijo; no se verificó si la plantilla muestra los pagos de hoteles. `[hipótesis]`
- No se verificó qué campo llena "Booked by" y "Booking confirmed for". `[hipótesis]`

## Pendientes
- [ ] Completar cliente y código de cliente cuando la usuaria los indique.

## Cómo validar
1. Abrir el PDF: 6 páginas; la página 2 tiene 7 capturas con números naranjas (1–8) y letras negras (A–F).
2. Emitir "IT: Total" desde una cotización y desde una reserva de prueba y comparar con el documento.

## Datos que pueden quedar viejos
- Tipografía y colores actuales de la plantilla — Georgia, #414042, #767171 — (foto al 2026-10-16)
- Imagen de portada actual — banner2.jpg 1140×785 — (foto al 2026-10-16)
