# Circuito sugerido para empresas receptivas — versión corta con marca Softur

- **Fecha:** 2026-11-16
- **Proyecto / cliente:** Softur — material genérico de implementación iTRAFFIC (receptivos)
- **Actualiza a:** [2026-11-16-circuito-sugerido-empresas-receptivas-parte-3.md](2026-11-16-circuito-sugerido-empresas-receptivas-parte-3.md)

## Objetivo
La versión de 3 páginas sobre la plantilla base salió con la estética Raleway/gris; la usuaria pidió "acordate de ponerle la marca Softur".

## Estado final
Terminado. `Trabajo/Entregables/Circuito sugerido para empresas receptivas (marca Softur).docx` (+ `.pdf`) reemplazados: 3 páginas, mismo contenido que la parte 3, con identidad de marca. Página 1: banda Tinta con logo, bajada "iTRAFFIC · Proceso administrativo contable", título en DM Serif Display. Página 2: diagrama con paleta de marca + secciones 00 a 03. Página 3: secciones 04 a 08.

## Decisiones y por qué
- Regla: estructura y extensión del documento base, pero estética siempre de marca Softur. `[decisión]` (pedido de la usuaria)
- Secciones numeradas 00–08 en Terracota + título DM Sans negrita; viñetas naranjas con tabulación (las líneas siguientes quedan alineadas). `[decisión]`
- Diagrama: cajas Arena `#F0ECE5`, borde `#C9C0B4`, fondo Marfil; las dos autorizaciones de pago resaltadas en naranja (`#E66B24` / `#FCE6D6`). `[decisión]`

## Archivos, tablas y objetos relevantes
- Paquete de marca: el de "Proceso de cancelaciones - Cuenca del Plata (marca Softur).docx" (sin el logo de Cuenca), encabezado "iTRAFFIC / Circuito sugerido para empresas receptivas", pie "Softur / Circuito administrativo contable · Uso confidencial".
- Generador (scratchpad, no persiste): `gen4.ps1` + `contenido4.ps1` + `Diagrama3.cs`.
- Softur.Serenity: no se consultó código nuevo.

## Cambios hechos
- Reemplazados el .docx y el .pdf en Entregables.

## Errores y cómo se resolvieron
- Las líneas que seguían dentro de una viñeta no quedaban alineadas con el texto — el "•" iba seguido de espacios — se cambió por "•" + tabulación con sangría francesa.

## Riesgos
- Letra chica en el diagrama (16 cm de ancho). `[hipótesis]`

## Pendientes
- [ ] Probar en base de prueba "?nro de planning" al imputar factura de proveedor — implementación.

## Cómo validar
1. PDF de 3 páginas, fondo Marfil, banda negra con logo, diagrama en la página 2.

## Datos que pueden quedar viejos
No aplica.
