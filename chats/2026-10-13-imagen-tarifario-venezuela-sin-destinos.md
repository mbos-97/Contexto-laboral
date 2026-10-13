# Imagen de tarifario Venezuela sin nombres de destinos

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Hover Tours (portada "Tarifario Venezuela 2026 - 2027")
- **Actualiza a:** No aplica

## Objetivo
Obtener la misma portada del tarifario pero sin los rótulos de destino sobre las tres fotos inferiores ("ISLA MARGARITA", "ISLA DE COCHE", "LOS ROQUES").

## Estado final
Terminado. Imagen generada en `../Tarifario-Venezuela-sin-destinos.jpg` (1280x720).

## Decisiones y por qué
- Se editó la imagen original en lugar de regenerarla: se borran sólo los rótulos y el resto queda idéntico (logo, título, fotos). `[decisión]`
- La edición se hizo con un script de PowerShell + C# (System.Drawing), porque en la PC no hay Python ni editor de imágenes por línea de comandos. `[datos]`

## Archivos, tablas y objetos relevantes
- `Trabajo/Tarifario-Venezuela-sin-destinos.jpg` — resultado.
- Softur.Serenity: no se consultó (la tarea no toca el sistema).

## Cambios hechos
- Se creó la imagen sin rótulos. No se modificó la original.

## Errores y cómo se resolvieron
- El script no compilaba en PowerShell 7 (faltan referencias de System.Drawing en .NET moderno) — se ejecutó con Windows PowerShell 5.1 (`powershell.exe`), donde `System.Drawing` alcanza como única referencia. `[datos]`

## Riesgos
- El relleno donde estaba el texto es una reconstrucción por difuminado: ampliando mucho se ve algo más suave en la zona de palmeras de la foto izquierda.
- La imagen de trabajo era de 1280x720; si existe un original de mayor resolución conviene repetir la edición sobre ese archivo.

## Pendientes
- No aplica.

## Cómo validar
Abrir la imagen y revisar la franja inferior de las tres fotos: no debe quedar texto ni manchas visibles.

## Datos que pueden quedar viejos
- Resolución de la imagen — 1280x720 — (foto al 2026-10-13)
