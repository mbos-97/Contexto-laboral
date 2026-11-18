# Maqueta de la ventana "Nuevo Cupos Servicios" en versión resumida

- **Fecha:** 2026-11-18
- **Proyecto / cliente:** Softur (servicios FD Glaciares Gourmet y Spirit; cliente no indicado)
- **Actualiza a:** No aplica

## Objetivo
Armar una imagen de la ventana "Nuevo Cupos Servicios" (se abre desde la Ficha Operativa) mostrando sólo un resumen por día y servicio: Fecha, Servicio, Total pasajeros y Cupos disponibles.

## Estado final
Terminado. Imagen en `Entregables/Maqueta Cupos Servicios resumido.png`.

## Decisiones y por qué
- Se respetó el aspecto de la ventana actual (barra azul con título y cruz, botón Excel, combo "Tipo", panel "Cupos Servicios") y se reemplazaron las columnas por las 4 pedidas. [decisión]
- Una línea por día y servicio, 2 días × 4 servicios: FD GLACIARES GOURMET CLASSIC, FD GLACIARES GOURMET PREMIUM, SPIRIT DELUXE, SPIRIT PREMIUM. Cantidades y fechas inventadas (18 y 19/11/2026). [decisión]

## Archivos, tablas y objetos relevantes
- `Entregables/Maqueta Cupos Servicios resumido.png`.
- Softur.Serenity: no se consultó (es una maqueta visual).

## Cambios hechos
- Se creó la maqueta en HTML y se exportó a PNG con Edge en modo headless (`--screenshot`, `--window-size=902,562`).

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Los números son ficticios; no presentarlos como datos reales.

## Pendientes
No aplica.

## Cómo validar
- Abrir el PNG y ver las 4 columnas y las 8 líneas.

## Datos que pueden quedar viejos
No aplica.
