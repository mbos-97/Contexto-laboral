# Itinerario AI: opcionales por reserva (campo "Código de opcionales") — factibilidad

- **Fecha:** 2026-10-19
- **Proyecto / cliente:** Latitud Ushuaia
- **Actualiza a:** [2026-10-19-itinerario-voucher-ai-latitud-ushuaia.md](2026-10-19-itinerario-voucher-ai-latitud-ushuaia.md)

## Objetivo
Saber si se puede agregar en la reserva un campo "Código de opcionales" donde se cargue un código de servicio para que ese servicio se muestre en un banner de opcionales dentro del itinerario.

## Estado final
Analizado. Hoy no existe; es un desarrollo a medida factible porque gran parte de la estructura ya está.

## Decisiones y por qué
- Los banners del itinerario salen de `BannerPage` vía el SP `BannerPage_Select` (lo llama la app externa del itinerario; no hay llamadas desde Serenity). [código]
- `BannerPage_Select` filtra por página (`nombrepage`, ej. `PRO2` = Tours opcionales), tipo de servicio, ciudad destino y, con `config BANNERPAGEXCLIENTE`, por cliente (`cod_agcia`). Recibe `@idreserva` pero **no lo usa para filtrar**: hoy los banners no cambian por reserva. [código]
- `BannerPage` ya tiene `idSearch`, que se usa para vincular un banner con un código de servicio (`Servicio_jSonFacility`: `s.Cod_serv = b.idSearch`, página `PRO1`, `config PRO1BANNERTOCLAVIS`). [código]
- La reserva no tiene un campo libre apto: "Otros datos" (`Reservaotrosdatos`) es para datos de pago (forma de pago, cuotas, moneda, URL). [código]
- Desarrollo propuesto: (1) campo nuevo en la reserva "Código de opcionales" (uno o varios códigos separados por guion); (2) `BannerPage_Select` con un modo para la página de opcionales que, si la reserva tiene códigos, devuelva sólo esos (banners con `idSearch` = código, o armados con nombre/foto/textos del servicio); (3) ajuste en la app Travel.Itinerary.AI para pasar la reserva y mostrar el bloque (su código no está en Serenity, lo estima desarrollo). [hipótesis]

## Archivos, tablas y objetos relevantes
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/BannerPage_Select.sql`
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Func/Servicio_jSonFacility.sql`
- `Softur.Serene.Model/Modules/E_Ventas/Entities/ReservaotrosdatosRow.cs`, `Softur.Serene.Web/Modules/E_Ventas/Reservaotrosdatos/`
- Tablas `BannerPage`, `Reserva`, `Reservaotrosdatos`, `config`.

## Cambios hechos
No aplica (sólo análisis).

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Requiere tocar la app del itinerario, fuera de Serenity: el alcance y el costo los define desarrollo. [hipótesis]
- Si se filtra la página PRO2 por reserva, hay que definir qué pasa cuando el campo está vacío (mostrar los generales o nada). [hipótesis]

## Pendientes
- [ ] Definir con el cliente: un código o varios, qué se muestra si está vacío, si el banner usa los datos del servicio o uno cargado aparte — comercial.
- [ ] Pedir estimación a desarrollo (Serenity + Travel.Itinerary.AI) — comercial.

## Cómo validar
Con el desarrollo hecho: cargar un código en la reserva de prueba y abrir el informe IT: el banner de opcionales debe mostrar sólo ese servicio.

## Datos que pueden quedar viejos
- Estado del SP `BannerPage_Select` — última migración `DefaultDB_20260819_180000_UpdateBannerPageSp` — (foto al 2026-10-19)
