# Nuevo proceso por sector — Cuenca del Plata: sólo proceso, con globos de escalamiento

- **Fecha:** 2026-10-27
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-27-nuevo-proceso-por-sector-cuenca-del-plata.md](2026-10-27-nuevo-proceso-por-sector-cuenca-del-plata.md)

## Objetivo
Reformular el documento: sacar los puntos a validar, dejar por página sólo el proceso de cada sector y sumar, por paso, qué pasa si no se puede cumplir y a quién se escala, en globos de texto con fondo de color.

## Estado final
Terminado. `Trabajo/Entregables/Nuevo proceso por sector - Cuenca del Plata (marca Softur).docx` (+ `.pdf`) reemplazado, 7 páginas: portada (circuito + cómo leer) · 01 Operaciones · 02 Proveedores · 03 Tesorería · 04 Reservas · 05 Administración · 06 Escalamiento en todo el circuito (tabla Problema / Lo detecta / Escala a / Si sigue).

## Decisiones y por qué
- Sin funciones, problemáticas ni objetivos ni puntos a confirmar: sólo pasos con responsable. `[decisión]` (pedido de la usuaria)
- Debajo de cada paso, dos globos: "¿Y si no se puede?" (fondo naranja claro `#FCE6D6`) y "Escalar a" (fondo Tinta `#191917`, texto Marfil). `[decisión]`
- Las respuestas de "¿y si no se puede?" y los escalamientos son **propuesta de Softur** (no salieron de la minuta): líder de Operaciones (Juan) para temas operativos, Comercial (costeo) para costos faltantes, Producto / Cargas para productos y tarifas, Cristian para Tesorería, "Responsable de Reservas" (no hay líder nombrado), Softur para fallas del sistema. `[hipótesis]`
- Contradicciones resueltas en el documento sin marcarlas: costea terceros **Comercial (costeo)** al día siguiente del servicio; asigna guías **Claudia** (Comercial deja de asignar). `[hipótesis]`
- Proveedores ya no "genera" la autorización: la genera iTraffic al guardar el planning; Proveedores la busca, controla y confirma. `[código]` (`iFichaopern_BloqueoAfterSave.sql`)
- Guías: el planning (`BloqueoRow`) tiene vehículo y chofer pero no guía; el guía va por ítem en la ficha operativa (un campo `guia` / `codguiaprov`). Para 2 o 3 guías se propone cargar el principal y el resto en la observación del planning hasta ajustar la orden de servicio (requiere desarrollo). `[código]`
- No se encontró en el código un estado "Falta vuelo": en el documento quedó como "revisar las reservas sin vuelo". `[código]` (búsqueda sin resultados en Model)

## Archivos, tablas y objetos relevantes
- Softur.Serenity (`git pull` previo): `Softur.Serene.Web/Modules/J_Receptivo/Bloqueo/BloqueoRow.cs` (campos del planning), `.../FichaOperativa/FichaOperativaRow.cs` y `FichaOperativaColumns.cs` (`Guia`, `CodGuiaprov`, `CodGuiaoper`), `iFichaopern_BloqueoAfterSave.sql` (autorización automática).
- Generador: `globos.ps1` + `contenido-globos.ps1` (scratchpad). Los globos son formas DrawingML `wedgeRoundRectCallout` en línea con cuadro de texto; el alto se calcula simulando el corte por palabras (sin autoajuste).

## Cambios hechos
- Documento reemplazado en Entregables (Word y PDF).

## Errores y cómo se resolvieron
- Primer cálculo del alto de los globos: sobraba espacio y Operaciones se pasaba de página; segundo: el texto se cortaba — se pasó a simular el corte por palabras (4,55 pt por carácter, 12,4 pt por línea).
- Globo ancho para "¿y si no se puede?" (3,5 M EMU) y angosto para "Escalar a" (2,05 M EMU), con el mismo alto.

## Riesgos
- Los escalamientos son propuesta: conviene validarlos con cada líder antes de difundir. `[hipótesis]`

## Pendientes
- [ ] Validar escalamientos y responsables con Cuenca del Plata — usuaria.
- [ ] Desarrollo: varios guías por ítem en la orden de servicio; corrección de la importación de facturas de proveedores — Softur.

## Cómo validar
1. PDF de 7 páginas; cada sector entra en una página; ningún globo corta texto.

## Datos que pueden quedar viejos
No aplica.
