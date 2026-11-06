# Correo de respuesta a Tolkeyen: estado de la encuesta de satisfacción

- **Fecha:** 2026-11-06
- **Proyecto / cliente:** Tolkeyen — encuesta de satisfacción a pasajeros (iTraffic)
- **Actualiza a:** No aplica

## Objetivo
Responder con firmeza, pero manteniendo las formas, el reclamo del cliente (correo del 04/11) por puntos pendientes de la encuesta y por la demora en la entrega.

## Estado final
Terminado: borrador de correo entregado en el chat para que la usuaria lo envíe.

## Decisiones y por qué
- Atributo "Encuestable" en Servicios › Parámetros: disponible en test. [decisión]
- Encuesta en formato responsive: disponible en test. [decisión]
- Reporte de encuestas con filtro de fecha (desde/hasta): disponible en test; se sugiere emitir en HTML o Excel, y en Word o PDF con página apaisada. [decisión]
- Pasar a producción requiere actualizar la versión del sistema; se propone el jueves 2026-11-12 y se pide confirmación al cliente. [decisión]
- Los puntos informados en la entrega anterior sin comentarios del cliente se dan por aprobados. [decisión]
- Cambio de la escala de recomendación (de 0-10, ya implementada como se pidió, a 1-5 con nuevos textos del box de comentarios): es una modificación sobre lo definido; se aborda recién después de poner en producción todos los puntos. [decisión]
- Nueva notificación por WhatsApp (recordatorio por fecha OUT): disponible a partir de la semana del 2026-11-09. [decisión]

## Archivos, tablas y objetos relevantes
- Entorno de test: iTraffic_Tolkeyentest (itraffic.dyndns.org).
- Pantallas: Encuestas (listado e informe "Encuestas con respuestas"), Servicios › Parámetros › "Encuestable".
- No se consultó Softur.Serenity (redacción de correo sobre estado informado por la usuaria).

## Cambios hechos
No aplica (sólo redacción del correo).

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Si el cliente no confirma el jueves 12/11, se demora la puesta en producción en plena temporada.
- El cliente puede insistir en que el cambio a escala 1-5 entre antes de producción.

## Pendientes
- [ ] Confirmación del cliente para actualizar versión en producción el jueves 2026-11-12 — Tolkeyen.
- [ ] Entregar la notificación por WhatsApp por fecha OUT — Softur — semana del 2026-11-09.
- [ ] Escala de recomendación 1-5 (1-2 "¿Qué podríamos haber hecho mejor?", 3 "¿Qué podríamos mejorar de su experiencia?", 4-5 "¿Qué fue lo que más valoró de su experiencia con Tolkeyen?") — Softur — después de producción.

## Cómo validar
En test: tildar "Encuestable" en un servicio y verificar que sólo aparezca en la encuesta si está en la reserva; abrir la encuesta desde un teléfono sin scroll horizontal; emitir el informe "Encuestas con respuestas" con filtro de fechas en HTML/Excel.

## Datos que pueden quedar viejos
- Fecha propuesta para producción — jueves 2026-11-12 — (foto al 2026-11-06)
