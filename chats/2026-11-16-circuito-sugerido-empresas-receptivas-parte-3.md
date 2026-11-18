# Circuito sugerido para empresas receptivas — rehecho sobre la plantilla base (3 páginas)

- **Fecha:** 2026-11-16
- **Proyecto / cliente:** Softur — material genérico de implementación iTRAFFIC (receptivos)
- **Actualiza a:** [2026-11-16-circuito-sugerido-empresas-receptivas.md](2026-11-16-circuito-sugerido-empresas-receptivas.md) y [parte 2](2026-11-16-circuito-sugerido-empresas-receptivas-parte-2.md)

## Objetivo
La usuaria rechazó la versión de 13 páginas ("no me gusta PARA NADA"): rehacerla por completo tomando como base `CLIENTES/Implementacion administrativa interna basica.pdf/.docx`, en 3 páginas como máximo.

## Estado final
Terminado. `Trabajo/Entregables/Circuito sugerido para empresas receptivas (marca Softur).docx` (+ `.pdf`) reemplazados: 3 páginas. Página 1: portada del base (logo Softur, "ITRAFFIC" naranja, título "Circuito sugerido para empresas receptivas"). Página 2: diagrama + Inicio (maestros), 1 Alta de Reserva, 2 Ficha Operativa. Página 3: 3 Planning, 4 Autorizaciones de Pago, 5 Facturas de Proveedores, 6 Pagos, 7 Cobros y Facturación, 8 Seguimiento y Control Diario.

## Decisiones y por qué
- Formato y tono del documento base: Raleway, títulos naranjas (`E97132`) numerados, viñetas cortas en infinitivo, justificado, logo en el encabezado de las páginas interiores. Pedido de la usuaria. `[decisión]`
- Diagrama redibujado con el estilo del base (cajas grises, sin colores por área); sólo las dos cajas de autorización de pago van resaltadas en naranja claro porque son el foco. `[decisión]`
- Se mantienen los datos de iTRAFFIC relevados antes (estado "Autorizar pago" → "OK", menús de Proveedores, búsqueda "?nro", botón "Autorizar"). `[código]` (ver memoria del circuito genérico)
- Se quitaron glosario, fichas por sección, tablas, recuadros y errores frecuentes. `[decisión]`

## Archivos, tablas y objetos relevantes
- Plantilla: `CLIENTES/Implementacion administrativa interna basica.docx` (portada en `w:sdt` "Cover Pages" con logo VML `rId7` + vínculo externo `rId8`; diagrama `rId9`; numeración: viñeta `numId 2`, sub-viñeta `numId 5` nivel 1; `titlePg`, encabezado con logo).
- Generador (scratchpad, no persiste): `gen3.ps1` + `contenido3.ps1` + `Diagrama2.cs` (Raleway medium `25787044783.ttf` de la caché de fuentes en la nube).
- Softur.Serenity: no se consultó código nuevo.

## Cambios hechos
- Reemplazados el .docx y el .pdf genéricos en Entregables.

## Errores y cómo se resolvieron
- El diagrama quedó en la portada — el `sdt` de portada no fuerza salto — `pageBreakBefore` en el párrafo del diagrama.
- Doble cierre `</w:body></w:document>` — el `sectPr` se tomó hasta el final del archivo — no volver a concatenar el final.

## Riesgos
- El diagrama, a 14 cm de ancho, tiene letra chica (igual que el base). `[hipótesis]`

## Pendientes
- [ ] Probar en base de prueba "?nro de planning" al imputar factura de proveedor — implementación (sigue de la memoria anterior).

## Cómo validar
1. PDF de 3 páginas con la estética del documento base y el diagrama en la página 2.

## Datos que pueden quedar viejos
No aplica.
