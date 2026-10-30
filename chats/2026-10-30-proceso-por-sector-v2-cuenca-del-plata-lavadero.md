# Proceso por sector v2 — Cuenca del Plata: VTV y lavadero con orden de compra

- **Fecha:** 2026-10-30
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-27-nuevo-proceso-por-sector-cuenca-del-plata-parte-3.md](2026-10-27-nuevo-proceso-por-sector-cuenca-del-plata-parte-3.md)

## Objetivo
Integrar al proceso de proveedores unas notas que la usuaria agregó al final de su Word: VTV y lavadero de vehículos con orden de compra, foto por lavado y proveedor con cuenta corriente.

## Estado final
Terminado. `Trabajo/Entregables/Proceso por sector v2 - Cuenca del Plata (marca Softur).docx` (+ `.pdf`, 13 páginas).

## Decisiones y por qué
- **Documento vigente:** `Proceso por sector v2 - Cuenca del Plata (marca Softur).docx`, editado por la usuaria (no generado por script). Reemplaza al "Nuevo proceso por sector". `[decisión]`
- Estructura de la v2 (hecha por la usuaria): 01 Reservas · 02 Operaciones (incluye Eugenia para Jungle Fly y Nils para VTV/lavadero) · 03 Administración, dividida por persona: Costeo (Facundo, costea al día siguiente lo prestado), Hoteles (Luz), Terceros, insumos y gastos (Giuliana), Entradas con precompra diaria (Grace), Guías (Jorge), Cuentas por cobrar (Romina y Daniela) · 04 Emisivo (Yamil controla las emisiones de Rosana) · 05 RRHH (Leo: sueldos, honorarios, impuestos) · 06 Tesorería (paga autorizaciones de Luz, Giuliana, Grace, Jorge, Víctor, Yamil y Leo; precompra de entradas contra la cuenta "Anticipo entradas"). El globo oscuro ahora dice "Recurrir a". `[decisión]`
- VTV y lavadero (Argentina y Brasil): Nils arma **un file por día** con todos los pedidos de compra del día y envía la orden de compra al proveedor (el lavadero trabaja con cuenta corriente); Giuliana autoriza el pago contra la orden de compra e **imputa en la factura el centro de costo de cada vehículo**; Tesorería paga la autorización. Por cada lavado se envía una foto que Nils registra en el file del día con el ID del formulario de revisión. `[decisión]`
- Se integró en el bloque de Giuliana: paso 4 reescrito y paso 5 nuevo (con sus globos). Las respuestas de los globos del paso 5 ("si no llega la foto no se autoriza ese lavado"; "Nils lo reclama al lavadero") son propuesta. `[hipótesis]`
- Se quitaron las notas sueltas del final. El paso 9 de Operaciones (Nils, reserva UC "con el valor de costo") no se tocó. `[decisión]`

## Archivos, tablas y objetos relevantes
- Scripts en el scratchpad: `integrar-lavadero.ps1` (edita el XML: clona el paso 4 para el 5, cambia texto en las dos copias de cada cuadro de texto —forma moderna y VML—, quita ids repetidos), `leer.ps1`, `outline.ps1`, `empaquetar.ps1`. Respaldo: `respaldo-proceso-v2-usuaria.docx`.
- Softur.Serenity: no se consultó (no se verificó si la reserva UC admite "orden de compra" como dato).

## Cambios hechos
- Word y PDF reemplazados en Entregables.

## Errores y cómo se resolvieron
- Al guardar en Word, cada globo queda duplicado (mc:AlternateContent con forma wps + VML de respaldo): hay que cambiar el texto en los dos.

## Riesgos
- Los pasos 4 y 5 de Giuliana quedan solos en la página 8 (la página 7 está llena). `[decisión]`
- No está verificado en iTraffic cómo se registra la orden de compra en la reserva UC. `[hipótesis]`

## Pendientes
- [ ] Alinear el paso 9 de Operaciones (Nils) con la orden de compra, si la usuaria lo pide.
- [ ] Verificar en Serenity dónde se carga la orden de compra y la foto en la reserva, y la imputación de centro de costo por vehículo en la factura de proveedor.

## Cómo validar
1. PDF página 8: pasos 4 (VTV y lavadero con orden de compra) y 5 (foto por lavado) de Giuliana, con globos.

## Datos que pueden quedar viejos
- Equipos por sector — (foto al 2026-10-30)
