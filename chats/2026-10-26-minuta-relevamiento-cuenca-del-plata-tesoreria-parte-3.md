# Minuta Cuenca del Plata: arranque con el circuito cruzado Operaciones, Proveedores y Tesorería

- **Fecha:** 2026-10-26
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria-parte-2.md](2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria-parte-2.md)

## Objetivo
Corrección de la usuaria: la implementación arranca el 2026-10-27 con el circuito cruzado Operaciones + pago a proveedores + Tesorería, y eso tiene que ir al principio del documento.

## Estado final
Terminado. 8 páginas. PDF reemplazado en `Trabajo/Entregables/Minuta de relevamiento - Cuenca del Plata (marca Softur).pdf`; el Word nuevo quedó como `... (marca Softur) v2.docx` porque el anterior estaba abierto en Word.

## Decisiones y por qué
- Primera etapa de la implementación (27/10): circuito cruzado Operaciones → Proveedores → Tesorería. Reservas y Administración quedan para después. `[decisión]`
- Nuevo orden: 01 Circuito cruzado, 02 Operaciones, 03 Proveedores, 04 Tesorería, 05 Reservas, 06 Administración, 07 Puntos a confirmar. La portada indica el inicio y el mapa de sectores tiene una columna "Etapa" (Arranque 27/10 / Siguiente / Antes de arrancar). `[decisión]`
- La sección 01 encadena lo acordado en la minuta: Operaciones carga el planning y emite la orden de servicio → Comercial costea terceros 1 día después y ajusta extras → Proveedores autoriza (solicitud + comprobante con número de planning) sólo el costo del file y el file se bloquea → Tesorería paga sólo autorizaciones, contra factura. Incluye "qué necesitamos para el primer día". `[decisión]`
- Coincide con lo relevado en código el 2026-10-15: el costeo del planning de la ficha operativa genera la autorización de pago al operador ([2026-10-15-circuito-operativo-itraffic-cuenca-del-plata.md](2026-10-15-circuito-operativo-itraffic-cuenca-del-plata.md)). `[código]`

## Archivos, tablas y objetos relevantes
- Generador: `minuta.ps1` (acepta `-Out`) + `contenido.ps1` en el scratchpad de la sesión.
- Softur.Serenity: no se consultó de nuevo.

## Cambios hechos
- PDF reemplazado; Word nuevo `Minuta de relevamiento - Cuenca del Plata (marca Softur) v2.docx`.

## Errores y cómo se resolvieron
- El .docx de destino estaba abierto en Word — se generó en el scratchpad y se copió como v2.

## Riesgos
- Quedan dos Word de la minuta en Entregables; el vigente es la v2. `[decisión]`
- El paso de costeo depende de definir si lo hace Operaciones o Comercial. `[hipótesis]`

## Pendientes
- [ ] Definir quién carga el costo de terceros antes del arranque — usuaria — 2026-10-27.
- [ ] Reemplazar el .docx viejo por la v2 cuando se cierre Word — usuaria.

## Cómo validar
1. Abrir el PDF: portada con "Inicio de la implementación" y columna "Etapa"; página 2 con el circuito cruzado de 4 pasos.

## Datos que pueden quedar viejos
- Fecha de arranque — 2026-10-27 — (foto al 2026-10-26)
