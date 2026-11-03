# Proceso de cancelaciones — Cuenca del Plata

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** No aplica (documento nuevo; complementa [2026-10-30-proceso-por-sector-v2-cuenca-del-plata-pedidos-de-carga.md](2026-10-30-proceso-por-sector-v2-cuenca-del-plata-pedidos-de-carga.md))

## Objetivo
Armar un documento nuevo, con la estética de "Proceso por sector v2", con el proceso de cancelaciones.

## Estado final
Terminado, con la política a definir. `Trabajo/Entregables/Proceso de cancelaciones - Cuenca del Plata (marca Softur).docx` (+ `.pdf`), 5 páginas: portada · 01 Política interna · 02 Sin penalidad · 03 Con penalidad · 04 Último minuto.

## Decisiones y por qué
- Política de cancelación interna: **a definir por Cuenca del Plata**; queda una tabla de plazos (hoteles / servicios × sin penalidad, con penalidad, último minuto) con "A definir". `[decisión]`
- Con anticipación, sin penalidad: Reservas cancela los ítems con costo y venta en 0. `[decisión]`
- Con tiempo y con penalidad: Reservas cancela el servicio con costo y venta en 0 y agrega el ítem "Gastos de cancelación" (si no existe, lo carga Cargas, pedido por correo al equipo de tarifas), ajustando costo y valor; si tiene costo, chequea el operador REAL al que hay que pagar (hotel o servicio). `[decisión]`
- Último minuto: Operaciones avisa a Reservas, que procede según la política. `[decisión]`
- Antes de esto se recomendó a la usuaria: Operaciones avisa, Reservas cancela y Administración define si queda con costo. `[hipótesis]`
- El contenido de los globos ("¿Y si no se puede?" / "Recurrir a") es propuesta. `[hipótesis]`
- "Se ajusta por costo y valor a llegar" se redactó como "hasta llegar al importe que corresponda". `[hipótesis]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity (`git pull` previo): `iFichaopern_BloqueoAfterSave.sql`: la autorización de pago (`autoriza`) se genera con el planning en estado `A`; con `R`, `M`, `1`, `3`, `4` se recalcula el costeo; en ese SP no hay baja ni reversa de `autoriza` (no se revisaron otros SP ni se probó). Por eso los globos piden avisar a Administración si el ítem ya tiene autorización. `[código]`
- Generador: `cancelaciones.ps1` + `contenido-cancelaciones.ps1` (scratchpad), base `base2` extraída de "Proceso por sector v2" (logos Softur + Cuenca del Plata, encabezado y pie).

## Cambios hechos
- Se creó el .docx y el .pdf. "Proceso por sector v2" no se tocó.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Falta probar qué pasa con una autorización ya generada si se cancela el ítem. `[hipótesis]`

## Pendientes
- [ ] Definir la política interna (plazos) — Cuenca del Plata.
- [ ] Definir cómo se autoriza y paga "Gastos de cancelación", y si "Servicios no prestados" se suma a este documento o a "Proceso por sector v2" — usuaria.
- [ ] Reexportar el PDF de "Proceso por sector v2", anterior a la última edición de la usuaria — usuaria / IA.

## Cómo validar
1. PDF de 5 páginas: portada con los casos; página 2 con la tabla "A definir"; páginas 3 a 5 con pasos y globos.

## Datos que pueden quedar viejos
No aplica.
