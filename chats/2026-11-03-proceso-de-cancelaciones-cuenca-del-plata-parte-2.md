# Proceso de cancelaciones — Cuenca del Plata: pago de los gastos de cancelación

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-11-03-proceso-de-cancelaciones-cuenca-del-plata.md](2026-11-03-proceso-de-cancelaciones-cuenca-del-plata.md)

## Objetivo
Definir cómo se autoriza y se paga el ítem "Gastos de cancelación".

## Estado final
Terminado. `Trabajo/Entregables/Proceso de cancelaciones - Cuenca del Plata (marca Softur).docx` (+ `.pdf`, 5 páginas). Sigue a definir la política interna.

## Decisiones y por qué
- "Gastos de cancelación" se autoriza y se paga a cada proveedor que corresponda. `[decisión]`
- Se agregó el paso 5 de la sección 03: autoriza quien controla ese proveedor y paga Tesorería (Responsable: Administración / Tesorería). Esa asignación sale del circuito de "Proceso por sector v2". `[hipótesis]`
- Globo del paso 5 (propuesta): si el comprobante no coincide con el costo del ítem, no se autoriza; recurrir a Reservas. `[hipótesis]`
- Fila 03 de la portada actualizada. `[decisión]`

## Archivos, tablas y objetos relevantes
- `contenido-cancelaciones.ps1` y `cancelaciones.ps1` (scratchpad). Softur.Serenity: no se consultó.

## Cambios hechos
- Word y PDF reemplazados en Entregables.

## Errores y cómo se resolvieron
- La herramienta PowerShell rechazó un comando largo por su texto ("Remove-Item on system path '/'"), sin ejecutar nada — se editó con la herramienta de edición y se corrió el generador en un comando simple.

## Riesgos
No aplica.

## Pendientes
- [ ] Definir la política interna (plazos) — Cuenca del Plata.
- [ ] Definir dónde va "Servicios no prestados" — usuaria.

## Cómo validar
1. PDF página 4: sección 03 con 5 pasos; el paso 5 es la autorización y el pago.

## Datos que pueden quedar viejos
No aplica.
