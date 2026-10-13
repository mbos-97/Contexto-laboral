# Guía rápida de Ficha Operativa: se agrega emisión de órdenes de servicio y pedidos a proveedores

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — material de usuario (iTraffic / Receptivo)
- **Actualiza a:** [2026-10-13-guia-rapida-ficha-operativa-con-marca.md](2026-10-13-guia-rapida-ficha-operativa-con-marca.md)

## Objetivo
Sumar a la guía rápida un apartado genérico sobre la emisión de órdenes de servicio y de pedidos de servicio a proveedor desde la Ficha Operativa.

## Estado final
Terminado. `Trabajo/Ficha operativa - Guia rapida.docx` pasó de 4 a 5 páginas y de 7 a 8 pasos.

## Decisiones y por qué
- El apartado nuevo es el paso 07 ("Emití órdenes de servicio y pedidos a proveedores"), ubicado después de armar el planning y antes de "Colores y guías" (que pasó a ser el 08), porque los documentos se emiten con vehículo, chofer y prestador ya asignados. `[decisión]`
- La redacción es genérica y no nombra reportes puntuales, porque la lista de reportes no está fija en el código: se carga por categoría desde la configuración de cada empresa y se filtra por permisos. `[código]`

## Archivos, tablas y objetos relevantes
Softur.Serenity consultado (sólo lectura, con `git pull` previo): `[código]`
- `Softur.Serene.Web/Modules/J_Receptivo/FichaOperativa/FichaOperativaGrid.ts`
  - Botón azul de impresión: `ReportHelper.addPrintDinamicToolbutton(..., 'FICHAOPE')`. Al emitir se envían la fecha desde/hasta, el filtro activo de la grilla y los ítems tildados.
  - Botón naranja "Pedidos": `mostrarDialogPedidos()`, toma todos los renglones que hay en pantalla.
- `Softur.Serene.Web/Modules/J_Receptivo/FichaOperativa/Pedido/` (`PedidoHelper.ts`, `PedidoEditor.ts`, `PedidoColumns.cs`) — la ventana de pedidos arma un renglón por operador/proveedor, con columna "Imprimir" que lista los reportes de la categoría `PEDIDOPER`.
- `Softur.Serene.Web/Modules/Common/Reporting/ReportHelper.ts` — los reportes dinámicos ofrecen salida PDF, Excel, Word, HTML y mail; con la configuración `IT_REPORTPERMISSION` se filtran por permiso `Reportes:<categoría>:<clave>`.

## Cambios hechos
- Se agregó el paso 07 con una captura recortada de la barra (botones de impresión y Pedidos), una tabla "Documento / Cómo se emite" y un recuadro de formatos.
- "Colores y guías" se renumeró a 08.

## Errores y cómo se resolvieron
- La tabla nueva quedaba partida entre dos páginas — se forzó salto de página antes del paso 07.

## Riesgos
- El nombre con el que aparece la orden de servicio en la lista del botón de impresión depende de cada empresa; la guía dice "elegí la orden de servicio" sin nombrar el reporte. `[hipótesis]`
- Que el reporte se limite a las reservas tildadas depende de cómo esté armado cada reporte; el código sólo garantiza que la selección se envía. `[código]`

## Pendientes
- [ ] Siguen abiertos los de la memoria anterior (capturas con datos de prueba; parte de configuración quitada).

## Cómo validar
1. Abrir el .docx: 5 páginas, pasos 01 a 08, paso 07 en la última página.
2. En un entorno de prueba, abrir Receptivo > Ficha Operativa y comprobar el botón azul de impresión y el botón naranja Pedidos.

## Datos que pueden quedar viejos
- Categorías de reportes `FICHAOPE` y `PEDIDOPER` — según el código al 2026-10-13
