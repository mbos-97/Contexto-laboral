# Itinerario "IT: Vouchers" (AI) de Latitud Ushuaia y su origen en Serenity

- **Fecha:** 2026-10-19
- **Proyecto / cliente:** Latitud Ushuaia
- **Actualiza a:** No aplica (complementa [2026-10-16-alta-itinerario-dinamico-ai-it-total-con-marca.md](2026-10-16-alta-itinerario-dinamico-ai-it-total-con-marca.md))

## Objetivo
Ver un itinerario publicado del cliente (vista `itxvoucher`, reserva de prueba) y ubicar de dónde sale en Softur.Serenity.

## Estado final
Terminado. Se leyó el itinerario en el navegador y se ubicó su definición en el repo.

## Decisiones y por qué
- La vista `typeview=itxvoucher` la sirve la app aparte `Travel.Itinerary.AI` (en el cliente, `iTraffic_<cliente>.AI/itinerary`); su código fuente **no** está en Softur.Serenity. [código]
- En Serenity sólo existe como informe web de reserva: `Informesweb` nombre `Rva_itxvoucheraliwen`, título "IT:Vouchers ALIWEN", módulo `RESERVA`, `sp` = URL `.../Travel.Itinerary.AI/itinerary?lang=en&typeview=itxvoucher&budget=0&id={id}` (`{id}` = id de reserva). [código]
- Contenido de la vista: bienvenida y textos fijos del cliente, contacto de operaciones, servicios por día con alojamiento, lugar de búsqueda, vuelo, horarios aproximados, cantidad de pax, observaciones de voucher, restricciones, y cierre con pedido de reseña. Sin precios (`budget=0`). [datos]

## Archivos, tablas y objetos relevantes
- `Softur.Serene/Softur.Serene.Model/Migrations/DefaultDB/Scripts/DefaultDB_20200417_104800_InformesWebItinerario.sql` (alta de los informes IT AI, incl. `Rva_itxvoucheraliwen`).
- Tabla `Informesweb` (campos `Nombre`, `Titulo`, `Modulo`, `sp`).
- `ScriptsBD/Sp_Configs/ConfigInsertsTextosItinerarios.sql` (textos de itinerarios).

## Cambios hechos
No aplica (sólo lectura).

## Errores y cómo se resolvieron
- Grep sobre todo el repo excede el tiempo — se usó `git grep`.

## Riesgos
- La URL del informe en el script apunta a otro dominio de cliente; en cada instalación se ajusta `sp` en `Informesweb`. [hipótesis]

## Pendientes
No aplica.

## Cómo validar
Abrir una reserva en iTraffic del cliente y buscar el informe IT de vouchers en Informes; debe abrir la misma URL con el id de la reserva.

## Datos que pueden quedar viejos
- Reserva de prueba consultada — id 53238, servicios 08 al 11/12/2026 — (foto al 2026-10-19)
