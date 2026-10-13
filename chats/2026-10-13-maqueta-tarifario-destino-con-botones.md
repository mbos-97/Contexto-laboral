# Maqueta: pantalla de destino del tarifario con botones Hoteles / Excursiones / Paquetes

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Tarifario web Softur (pantalla de destino "Isla de Margarita - El Yaque")
- **Actualiza a:** No aplica (misma sesión que [2026-10-13-imagen-tarifario-venezuela-sin-destinos.md](2026-10-13-imagen-tarifario-venezuela-sin-destinos.md))

## Objetivo
Armar una maqueta de la pantalla de destino del tarifario con tres botones en fila (apaisados) debajo de la imagen del destino, en el pie: Hoteles, Excursiones y Paquetes.

## Estado final
Terminado. Maqueta en `../Tarifario-destino-con-botones.png` (1882x897). Es una imagen editada, no un cambio en el sistema.

## Decisiones y por qué
- Los tres botones van centrados en la franja del pie, entre el copyright y los links de Privacy/Terms, sin mover el resto de la pantalla. `[decisión]`
- Hoteles y Excursiones son los botones reales de la captura que pasó la usuaria; Paquetes no existía como botón y se armó con el mismo marco y el ícono + texto "Paquetes" del menú lateral, para que quede con el mismo estilo. `[decisión]`
- El color de fondo de los botones y el del menú lateral son el mismo (RGB 1, 6, 89). `[datos]`

## Archivos, tablas y objetos relevantes
- `Trabajo/Tarifario-destino-con-botones.png` — maqueta.
- Softur.Serenity: no se consultó (no se pidió nada sobre el funcionamiento del sistema, sólo la imagen).

## Cambios hechos
- Se creó la maqueta. No se modificaron las capturas originales ni código.

## Errores y cómo se resolvieron
- `System.Drawing` no lee WebP — se convirtió la captura a PNG con WIC (`System.Windows.Media.Imaging.BitmapDecoder`) desde `powershell.exe`. `[datos]`
- En scripts de PowerShell no nombrar una función `R`: es alias de `Invoke-History`. `[datos]`

## Riesgos
- El botón Paquetes es una reconstrucción: ampliando mucho, su texto se ve apenas más suave que el de los otros dos.
- La maqueta no implica que el tarifario web ya soporte ese botón; si se quiere implementar hay que revisarlo en el código.

## Pendientes
- [ ] Si la maqueta se aprueba, relevar en Softur.Serenity cómo se definen los botones del pie del tarifario — sin responsable ni fecha.

## Cómo validar
Abrir la imagen y revisar el pie: tres botones alineados, mismo alto y color, centrados bajo la imagen del destino.

## Datos que pueden quedar viejos
- Tamaño de la captura — 1882x897 — (foto al 2026-10-13)
