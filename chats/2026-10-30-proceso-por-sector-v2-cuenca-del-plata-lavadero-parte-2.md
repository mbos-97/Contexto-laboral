# Proceso por sector v2 — Cuenca del Plata: paso de Nils en Operaciones alineado

- **Fecha:** 2026-10-30
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-30-proceso-por-sector-v2-cuenca-del-plata-lavadero.md](2026-10-30-proceso-por-sector-v2-cuenca-del-plata-lavadero.md)

## Objetivo
Alinear el paso 9 de Operaciones (Nils, VTV y lavadero) con el circuito de orden de compra que quedó en el bloque de Giuliana.

## Estado final
Terminado. `Trabajo/Entregables/Proceso por sector v2 - Cuenca del Plata (marca Softur).docx` (+ `.pdf`, 13 páginas) actualizado.

## Decisiones y por qué
- Paso 9 de Operaciones: Nils arma un file por día con todos los pedidos de compra del día, envía la orden de compra al proveedor y registra en el file la foto de cada lavado con el ID del formulario de revisión; Giuliana autoriza y Tesorería paga. Globo: si no tiene el pedido de compra o el comprobante, no lo carga hasta tenerlo; recurrir a Giuliana (sin cambios). `[decisión]`
- Se quitó la mención a "reserva de tipo UC" del paso 9, para usar el mismo término ("file") que el paso 4 de Giuliana. `[decisión]`

## Archivos, tablas y objetos relevantes
- Script `alinear-nils.ps1` (scratchpad). Softur.Serenity: no se consultó.

## Cambios hechos
- Word y PDF reemplazados en Entregables.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- En el paso 6 de Operaciones el globo oscuro dice "RECURRIR" sin la "A" (texto de la usuaria, no se tocó). `[decisión]`

## Pendientes
- [ ] Verificar en Serenity si el "file diario" de Nils es una reserva de tipo UC y dónde se cargan orden de compra, foto y centro de costo — Softur.

## Cómo validar
1. PDF página 5: paso 9 de Nils con file diario, orden de compra y foto.

## Datos que pueden quedar viejos
No aplica.
