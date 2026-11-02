# Manual de Servicio online: términos generalizados

- **Fecha:** 2026-11-02
- **Proyecto / cliente:** Softur — material técnico genérico (webservices de cobro online)
- **Actualiza a:** [2026-11-02-manual-servicio-online-marca-softur.md](2026-11-02-manual-servicio-online-marca-softur.md)

## Objetivo
Quitar del manual los términos que delatan el país de origen.

## Estado final
Terminado. PDF y .docx regenerados sobre los mismos archivos, 13 páginas.

## Decisiones y por qué
- `FacturaDGI` pasa a `FacturaFiscal` y "Número de factura DGI" a "Número de factura fiscal" — pedido de la usuaria. `[decisión]`
- "Cédula de identidad" pasa a "Documento de identidad" y "Rut" a "Identificación tributaria"; los códigos (1 y 4) no cambian. `[decisión]`

## Archivos, tablas y objetos relevantes
- `Entregables/Manual servicio online (marca Softur).pdf` y `.docx`.
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/Redpagos_consulta.sql`: el campo real sigue siendo `FacturaDGI`. `[código]`

## Cambios hechos
- Se actualizaron los dos entregables. El repo Softur.Serenity no se tocó.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- `FacturaFiscal` no coincide con el campo real `FacturaDGI`: un integrador que siga el manual contra el servicio actual puede no encontrarlo. `[código]`

## Pendientes
- [ ] Antes de usar el manual en una integración real, avisar la diferencia de `FacturaFiscal` y confirmar la dirección — usuaria.

## Cómo validar
1. Buscar en el .docx "DGI", "Cédula" y "Rut": no debe haber resultados.

## Datos que pueden quedar viejos
- Cantidad de páginas — 13 — (foto al 2026-11-02)
