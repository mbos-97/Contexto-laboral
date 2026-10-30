# Proceso por sector v2 — Cuenca del Plata: Administración por persona, Costeo (Facundo), RRHH y logo de Cuenca

- **Fecha:** 2026-10-29
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-27-nuevo-proceso-por-sector-cuenca-del-plata-parte-3.md](2026-10-27-nuevo-proceso-por-sector-cuenca-del-plata-parte-3.md)

## Objetivo
Con una minuta nueva de relevamiento (pegada por la usuaria), armar un documento sector por sector, parecido al "Nuevo proceso por sector", con sólo lo que cada área empieza a hacer (sin lo actual) y a quién recurrir si un paso no se cumple. Orden pedido: Reservas → Operaciones → Administración (por persona) → RRHH → Tesorería. Con el logo de Cuenca del Plata.

## Estado final
Terminado. `Trabajo/Entregables/Proceso por sector v2 - Cuenca del Plata (marca Softur).docx` (+ `.pdf`), 13 páginas: portada (logos Softur + Cuenca, regla de oro, circuito, cómo leer) · 01 Reservas · 02 Operaciones · 03 Administración (rutina diaria + Costeo·Facundo, Hoteles·Luz, Terceros/insumos/gastos·Giuliana, Entradas·Grace, Guías·Jorge, Cuentas por cobrar·Romina y Daniela) · 04 RRHH · 05 Tesorería · 06 A quién recurrir (tabla). El documento del 27/10 editado por la usuaria no se tocó.

## Decisiones y por qué
- Funciones definidas por la usuaria: Luz chequea todos los costeos de hoteles, pide a Ventas o Tarifas si no coinciden y autoriza el pago; Giuliana costea a diario con Facundo los servicios de terceros del día anterior, chequea costos, carga autorizaciones, y además facturas y autorizaciones de insumos/gastos; Grace controla las entradas del día, hace el pedido, registra la autorización y costea/genera los plannings de las entradas del día anterior; Jorge costea los guías del día anterior y genera sus autorizaciones; Romina y Daniela controlan cuentas por cobrar; **Costeo = Facundo**: saca la planilla de servicios del día anterior, completa lo faltante con Administración y genera el costeo de todo. `[decisión]`
- Proveedores dejó de ser un sector: Luz y Giuliana quedaron dentro de Administración. `[decisión]`
- Se mantuvieron los cambios propios de la usuaria del documento anterior: datos faltantes de la reserva completos 96 h antes, vuelos reconfirmados **72 h** antes (la minuta nueva dice 24 h; se dejó 72 h y se le avisó), Facundo como costeo. `[decisión]`
- Globo "Escalar a" renombrado "Recurrir a" (palabra de la usuaria). Los "¿y si no se puede?" y a quién recurrir siguen siendo **propuesta de Softur**. `[hipótesis]`
- No se incluyó "que Reservas pueda asignar guías desde los plannings" porque contradice "se centraliza todo en Claudia"; quedó para que la usuaria lo defina. `[decisión]`
- "Falta vuelo" se nombró como estado, tal como lo pide la minuta (en el código no existe; ver memoria del 27/10). `[hipótesis]`

## Archivos, tablas y objetos relevantes
- Logo de Cuenca del Plata guardado en `Contexto-laboral/recursos/logo-cuenca-del-plata.jpeg` (JPEG 250×117, fondo blanco; original en `Downloads/WhatsApp Image 2026-10-13 at 16.44.20.jpeg`). En la portada va en una celda blanca a la derecha de la banda Tinta de Softur.
- Base OOXML: el paquete del "Nuevo proceso por sector" (estilos, encabezado, pie, logo Softur). Scripts en el scratchpad de la sesión: `globos.ps1` (generador), `funciones-globos.ps1` (Paso, Globo, Rol), `contenido-v2.ps1` (contenido), `pdf2png.ps1`.
- Softur.Serenity: no se consultó (se reutilizaron los hallazgos de código del 27/10).

## Cambios hechos
- Documento nuevo en Entregables (Word y PDF).

## Errores y cómo se resolvieron
- Globos separados de su paso en el salto de página: hay que poner `keepNext` en **todos** los párrafos de la tabla del paso (también en la celda del número), no sólo en el primero.
- El harness bloqueó un comando de PowerShell que incluía `Remove-Item` con comodín; se resolvió escribiendo los ajustes en un .ps1 y ejecutándolo.

## Riesgos
- Las vías de "recurrir a" son propuesta: validarlas con cada líder antes de difundir. `[hipótesis]`

## Pendientes
- [ ] Validar con la usuaria: 72 h vs 24 h para reconfirmar vuelos; si Reservas puede asignar guías desde el planning; nombre del responsable de Reservas y de RRHH — usuaria.

## Cómo validar
1. PDF de 13 páginas; portada con los dos logos; ningún globo separado de su paso.

## Datos que pueden quedar viejos
No aplica.
