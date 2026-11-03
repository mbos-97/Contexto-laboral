# Mapa de vehículos — Cuenca del Plata

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-11-03-movimientos-internos-moviles-cuenca-del-plata.md](2026-11-03-movimientos-internos-moviles-cuenca-del-plata.md)

## Objetivo
Definir cómo registrar los móviles que no están en servicio.

## Estado final
Idea definida por la usuaria; desarrollo sin relevar ni estimar. Reemplaza la recomendación de un file "Móvil fuera de servicio".

## Decisiones y por qué
- Desarrollar un **mapa de vehículos**: por día, cada unidad con sus servicios asignados y horarios, un tilde de no disponible y un comentario con el motivo. `[decisión]`
- Los movimientos internos siguen con un file por salida y su planning. `[decisión]`
- El planning (`bloqueo`) ya tiene vehículo, chofer, fecha y hora desde/hasta; no se encontró dónde guardar la no disponibilidad ni si bloquearía la asignación. `[código]`

## Archivos, tablas y objetos relevantes
- `Softur.Serene.Web/Modules/J_Receptivo/Bloqueo/BloqueoRow.cs`. No se consultó código nuevo.

## Cambios hechos
No aplica.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
No aplica.

## Pendientes
- [ ] Definir el alcance del mapa (por rango de fechas u horas, si bloquea la asignación) y pedir estimación a desarrollo — usuaria.

## Cómo validar
No aplica.

## Datos que pueden quedar viejos
No aplica.
