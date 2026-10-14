# Comprobante de alta del Itinerario dinámico (IT Total) con identidad Softur

- **Fecha:** 2026-10-14
- **Proyecto / cliente:** Softur — alta de producto Itinerario dinámico (iTraffic), cliente De la Paz Tour
- **Actualiza a:** No aplica

## Objetivo
Rehacer el documento de alta del Itinerario dinámico "IT Total" con la identidad de marca Softur, separando lo que el cliente tiene que enviar de lo que ya sale de iTraffic / Serenity.

## Estado final
Terminado. Se entregó `Trabajo/Alta Itinerario dinamico IT Total - De la Paz (marca Softur).docx` (8 páginas A4, editable) y su PDF.

## Decisiones y por qué
- Estructura: portada con datos del cliente, recuadro "Importante" y leyenda de etiquetas; 01 mapa del itinerario + tabla "Quién define cada parte"; 02 lo que envía el cliente; 03 lo que se carga en iTraffic; 04 checklist de envío. `[decisión]` (criterio propio, la usuaria pidió distinguir Serenity vs. cliente)
- Dos etiquetas visibles en cada punto: "ENVÍA EL CLIENTE" (Terracota sobre Arena) y "SE CARGA EN iTRAFFIC" (Marfil sobre Tinta). `[decisión]`
- Se mantuvo la numeración de las capturas anotadas del documento original (1–9 y secciones A–E) para que las referencias coincidan. La tipografía, que en el original era "5" pero no tenía marca en la imagen, pasó a "F". `[decisión]`
- Se reutilizaron las capturas del documento original (mapa anotado y formularios BannerPage PRO1/PRO2) porque las capturas del navegador integrado salían recortadas. `[decisión]`
- El texto sobre la imagen se pide en dos líneas (frase + palabra destacada), porque así se muestra en el itinerario de prueba. `[datos]`
- Se mantuvo cliente "De la Paz Tour" y su código de cliente del documento original (dato de empresa, no personal). `[decisión]`

## Qué es del cliente y qué sale del sistema
- **Envía el cliente:** logo `logoheader.png` (576×208, 32 KB), imagen `banner.jpg` (3200×800, 230 KB), texto sobre la imagen, color HEX de barra superior y pie, nombres de las 5 secciones, íconos `ico1..ico4.png` (300×300, 20 KB) con título y leyenda, fuente, contacto, redes, WhatsApp, fotos opcionales. `[datos]` (specs tomadas del documento original)
- **Sale de iTraffic:** `[código]`
  - Visión general, cronograma y detalle por día: datos de la reserva.
  - Título y descripción de cada día: textos del servicio configurados en `config` `ITNAME<idioma>` (código 72, "TITULO IT"), `ITVOUC<idioma>` (74, "DETALLE IT"), `ITWEB<idioma>`; `TEXTOSERVICIO` 78 = "VOUCHER IT". Los lee `ifsp_GetDatosDet_rvait`.
  - Sección "Información útil" = banners `BannerPage` con Página del banner `PRO1` ("PROMO 1"); "Tours opcionales" = `PRO2` ("PROMO 2"). Parámetro `parame` código `PBNN`.
  - El itinerario se abre desde la reserva con el informe web `Rva_itxfull`, título "IT: Total" (`informesweb`, URL `<RUTAURLBASEITINERARIO>/itinerary?...typeview=itxfullend...`; requiere `config` `LITINERARIOMODULOACTIVO = .T.`).

## Archivos, tablas y objetos relevantes
- Origen: `Descargas/ALTA IT TOTAL DINÁMICO - DE LA PAZ .docx`; itinerario de prueba en `test.ringo.softur.com.ar/Travel.Itinerary.Enterprise.Dinamico/itinerary?...typeview=itxfull...` (reserva de prueba).
- Softur.Serenity consultado (sólo lectura, con `git pull` previo): `[código]`
  - `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Tables/BannerPage.sql` — tabla `BannerPage` (nombrepage, ordenpage, urlimagen..urlimagen4, nombrebanner, precio, moneda, fechadesde/hasta, observaciones, cod_agcia).
  - `Softur.Serene.Web/Modules/L_Configuraciones/BannerPage/BannerPageForm.generated.cs` — campos del formulario y pestañas General / Observaciones Web / Imagenes, editor Textgen (`BANNERPAGE`).
  - `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp_Configs/ParameDefaultInsert.sql` — valores `PBNN` (PRO1, PRO2, HOME, CARR, HDES, etc.).
  - `.../Sp_Configs/ConfigInsertsTextosItinerarios.sql` y `.../Func/ifsp_GetDatosDet_rvait.sql` — textos del servicio para el itinerario.
  - `.../Scripts/DefaultDB_20200417_104800_InformesWebItinerario.sql` — alta del informe "IT: Total".
  - El proyecto web `Travel.Itinerary.Enterprise.Dinamico` (Umbraco) **no está** en Softur.Serenity; colores, textos de la barra y pie se configuran fuera de este repo. `[hipótesis]`

## Cambios hechos
- Se creó el .docx nuevo y su PDF. No se modificó el original ni Softur.Serenity.

## Errores y cómo se resolvieron
- En PowerShell, funciones llamadas `R` y `CP` chocan con alias (`r` = Invoke-History, `cp` = Copy-Item) — se renombraron a `Rn` y `CPar`.
- Capturas del navegador integrado a 1280 px salían recortadas o con timeout — se usaron las capturas del documento original.
- Algunas líneas de tabla de 0,5 pt no se veían en el render — se subió el borde a 1 pt.

## Riesgos
- En el itinerario de prueba la 4.ª sección dice "Visión General" pero apunta a "Por qué nosotros" (#aboutus); "Información útil" y "Tours opcionales" muestran tarjetas duplicadas; el botón de WhatsApp no tiene número (`wa.me/?text=`); el pie muestra datos de contacto de Softur. Son datos de la demo, no del cliente. `[datos]`
- Las capturas anotadas son de una demo con destinos y datos de ejemplo; si el documento se comparte con otros clientes conviene revisarlas. `[hipótesis]`

## Pendientes
- [ ] Confirmar con la usuaria si el documento se usa como plantilla genérica para otros clientes (hoy dice De la Paz Tour).
- [ ] Confirmar si las fechas desde/hasta del banner filtran lo que se muestra (no verificado en el SP `BannerPage_Select`).

## Cómo validar
1. Abrir el .docx: 8 páginas, fondo Marfil, título en serif, secciones 01–04, etiquetas en cada punto.
2. En un entorno de prueba, abrir una reserva y emitir "IT: Total"; comprobar que Información útil muestra los banners PRO1 y Tours opcionales los PRO2.

## Datos que pueden quedar viejos
- Tipografía actual del itinerario de prueba — Roboto — (foto al 2026-10-14)
- Specs de archivos (logo, banner, íconos) — según el documento original — (foto al 2026-10-14)
