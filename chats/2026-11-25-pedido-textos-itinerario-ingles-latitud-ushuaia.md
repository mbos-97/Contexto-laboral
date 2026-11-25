# Pedido de textos fijos en inglés del itinerario de vouchers de Latitud Ushuaia

- **Fecha:** 2026-11-25
- **Proyecto / cliente:** Latitud Ushuaia (código 05071)
- **Actualiza a:** No aplica (complementa [2026-10-19-itinerario-voucher-ai-latitud-ushuaia.md](2026-10-19-itinerario-voucher-ai-latitud-ushuaia.md))

## Objetivo
Armar el documento para pedirle a Latitud la traducción al inglés de los textos fijos del itinerario de vouchers (lo que no se carga en iTRAFFIC).

## Estado final
Terminado. Documento listo para enviar: `Trabajo/Entregables/Pedido de textos del itinerario en ingles - Latitud Ushuaia (marca Softur).docx` y `.pdf` (3 páginas).

## Decisiones y por qué
- El itinerario instalado (`iTraffic_Latitud.AI/itinerary?typeview=itxvoucher`) sale entero en español aun con `lang=en`: textos fijos, rótulos y fechas. [datos]
- Los textos fijos y las imágenes viven en el formato instalado (carpeta `Agents/05071/img` de la app AI: `LogoLatitud.png`, `banner.png`, `Contanos.png`), no en Softur.Serenity ni en iTRAFFIC. [código] [datos]
- Se piden: bienvenida (título, 4 párrafos, 2 viñetas de horario), título "SU ITINERARIO EN USHUAIA", rótulos del servicio (Lugar de búsqueda, Hora aproximada de búsqueda, Vuelo, Número de pasajeros, Observaciones, Alojamiento, leyenda de restricciones de salud), textos de guía y reseñas, cierre, enlace de la guía en inglés y los dos banners en PNG en inglés (706×211 y 707×210, tienen el texto dentro de la imagen). [decisión]
- Los datos de reserva y servicios quedan fuera del pedido (salen de iTRAFFIC). [decisión]
- Formato: formulario de marca Softur reutilizando el paquete del formulario de facturación electrónica Uruguay; tabla de 3 columnas (dónde se ve / español / inglés a completar); sin "Próximos pasos". [decisión]

## Archivos, tablas y objetos relevantes
- Itinerario de prueba: reserva id 54119 (`lang=es` y `lang=en`).
- Documentos previos del cliente: `CLIENTES/LATITUD/Alta - Voucher itinerario.docx` y `Modificaciones itinerario.docx` (texto de bienvenida, guía y reseñas pedidos por Latitud).
- Softur.Serenity: `git grep` de "Fin del Mundo" / "Lugar de búsqueda" sin resultados en templates del itinerario; sólo `Softur.Serene.Model/Migrations/DefaultDB/Scripts/DefaultDB_20200417_104800_InformesWebItinerario.sql` (informe `Rva_itxvoucheraliwen`).
- Paquete base: `Entregables/Configuracion Facturacion Electronica Uruguay DGI (marca Softur).docx`.

## Cambios hechos
- Se creó el .docx y el .pdf del pedido en `Entregables`.

## Errores y cómo se resolvieron
- La reserva de prueba 53238 ya no carga datos — se usó la 54119 que abrió la usuaria.
- Al correr el script con `powershell.exe` 5.1 se rompieron los acentos — correrlo con PowerShell 7 (pwsh).
- Renglones con `<w:br/>` en celdas justificadas se estiran — usar un párrafo por renglón.

## Riesgos
- La leyenda de restricciones de salud no se vio en la reserva de prueba; su texto exacto en español no está relevado. [hipótesis]
- Fechas y días ("Miércoles 18 de noviembre") también salen en español con `lang=en`; no se pidieron al cliente porque son del sistema. [hipótesis]

## Pendientes
- [ ] Enviar el pedido a Latitud y, con la respuesta, pedir a desarrollo la versión en inglés del formato — usuaria.

## Cómo validar
1. Abrir el .pdf en `Entregables` y verificar 3 páginas con las secciones 01 a 05.
2. Comparar los textos en español con el itinerario `lang=es` de la reserva 54119.

## Datos que pueden quedar viejos
- Reserva de prueba — id 54119, servicios 18 al 21/11/2026 — (foto al 2026-11-25)
- Medidas de los banners — 706×211 y 707×210 px — (foto al 2026-11-25)
