# Circuito operativo iTraffic para Cuenca del Plata: versión esquematizada con diagrama

- **Fecha:** 2026-10-15
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-15-circuito-operativo-itraffic-cuenca-del-plata.md](2026-10-15-circuito-operativo-itraffic-cuenca-del-plata.md)

## Objetivo
Hacer el documento más esquemático y fácil de leer: empezar con un diagrama como el del documento base, con proceso y responsable explícitos, y extender la información a partir de ese cuadro, sin datos irrelevantes.

## Estado final
Terminado. 5 páginas (antes 10). `Trabajo/Entregables/Circuito operativo iTraffic - Cuenca del Plata.pdf` actualizado; el Word nuevo quedó como `... v2.docx` porque el .docx anterior estaba abierto en Word.

## Decisiones y por qué
- Página 1: diagrama de flujo propio (basado en el del documento base) donde el **color de la caja indica el responsable** (Arena = Producto + Data entry, naranja claro = Ventas, Tinta = Operaciones, blanco con borde terracota = Administración) y un número remite al cuadro de procesos. `[decisión]` (pedido de la usuaria)
- El diagrama corrige el base: las cuentas por pagar salen del **costeo de la ficha operativa**, no del ingreso de la reserva. `[código]` (ver memoria anterior, `iFichaopern_BloqueoAfterSave.sql`)
- Página 2: cuadro "Procesos y responsables" con 8 procesos (01 Maestros, 02 Reserva, 03 Ficha operativa, 04 Cobros, 05 Facturación, 06 Facturas de proveedores, 07 Pagos, 08 Caja). `[decisión]`
- El detalle pasó a cuadros cortos; las etapas administrativas se agruparon en una sola tabla (04–08). Se quitaron "Cómo leer", "Próximos pasos", consejos generales (duplicados, límites de crédito), formatos de salida y menciones a configuraciones internas. `[decisión]`
- Se afirma que el costo del planning va al operador del vehículo (la autorización de pago toma el operador del prestador del vehículo). `[código]`

## Archivos, tablas y objetos relevantes
- Documento base: imagen del diagrama dentro de `CLIENTES/Circuito basico sugerido iTRAFFIC.docx` (`word/media/image2.jpeg`).
- Softur.Serenity: no se consultó código nuevo; se reutilizó lo relevado en la memoria anterior.

## Cambios hechos
- PDF reemplazado en Entregables; Word nuevo `Circuito operativo iTraffic - Cuenca del Plata v2.docx`. El .docx de 10 páginas quedó sin tocar (estaba abierto).

## Errores y cómo se resolvieron
- DM Sans no está instalada en Windows: Word la usa desde la caché de fuentes en la nube de Office (`%LOCALAPPDATA%\Microsoft\FontCache\4\CloudFonts\DM Sans`). Para dibujar con `System.Drawing` se cargan esos .ttf con `PrivateFontCollection`, **cada estilo en su propia colección** (todos se registran como "Regular"; juntos, GDI+ usaba la itálica).
- En PowerShell, `(… | Where-Object …)[0]` sobre un único resultado devuelve el primer carácter del string — usar `@(…)[0]`.
- El .docx destino estaba abierto en Word — se generó en el scratchpad y se guardó como v2.

## Riesgos
- Quedan dos Word en Entregables (versión larga y v2). Conviene borrar el viejo cuando la usuaria lo cierre. `[decisión]`
- Siguen los riesgos de la memoria anterior (honorario del guía como costo extra es recomendación; ejemplo de tarifas ilustrativo). `[hipótesis]`

## Pendientes
- [ ] Confirmar responsables de 04–08 con Cuenca del Plata — usuaria.
- [ ] Reemplazar el .docx viejo por la v2 — usuaria.

## Cómo validar
1. Abrir el PDF: página 1 con el diagrama y la leyenda de colores; página 2 con el cuadro de 8 procesos; 5 páginas en total.

## Datos que pueden quedar viejos
No aplica.
