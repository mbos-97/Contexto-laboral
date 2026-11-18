# Manual de uso iConnect Marpatag v0.2 — formato Caracol y capturas en alta resolución

- **Fecha:** 2026-11-13
- **Proyecto / cliente:** Marpatag — iConnect (venta web B2B sobre iTraffic)
- **Actualiza a:** [2026-11-13-manual-uso-iconnect-marpatag-parte-2.md](2026-11-13-manual-uso-iconnect-marpatag-parte-2.md)

## Objetivo
Las capturas se veían mal. La usuaria pasó como modelo de contenido (no de estética) un manual que armaba a mano: "M-CLAVIS CUSTOMIZACION CARACOL" (37 páginas).

## Formato a replicar (manual Caracol) `[decisión]`
- Las secciones arrancan por la configuración en iTraffic (alta de usuarios en Ventas › Contacto Clientes con sus solapas, tipo de reserva web, imágenes y banners, destinos publicados) y siguen por la web (inicio, actividades, hoteles, proceso de compra, autogestión).
- Cada elemento de la web lleva una letra o un número en un **recuadro rojo**. Debajo, cada letra explica de dónde sale el dato, con la **captura de la pantalla de iTraffic** donde se carga y el campo marcado en rojo.
- "Consideraciones a tener en cuenta" para que un servicio aparezca (activo, tarifa vigente, publicar, venta distinta de 0) y avisos "Importante".

## Estado final
Hecho. Manual v0.2 regenerado, 22 páginas: `Entregables/Manual de uso iConnect - Venta web B2B - Marpatag (marca Softur).docx` + PDF. Lleva 30 capturas en alta resolución (17 de iConnect y 13 de iTraffic) con recuadros rojos, y datos sensibles ocultos (pasajero, vendedor, cuenta bancaria, clave web). Secciones: 01 Alta de usuarios, 02 Tipo de reserva web, 03 Inicio, 04 Qué tiene que tener cargado el servicio, 05 Búsqueda y resultados, 06 Detalle, 07 Proceso de compra, 08 Mi panel y reservas, 09 Mis datos, 10 Configs, 11 Pendientes.

## Hallazgos en iTraffic Marpatag (pantallas) `[datos]`
- Usuario iConnect = **contacto** del cliente (Ventas › Contacto Clientes): solapa Generales (Cliente), Datos de logueo (Usuario Web, Clave Web, **Usuario Validado**, Vendedor preferente), Atributos Web (Ver Tarifas, Enviar factura, Ver Reservas propias, Ver Reservas de su empresa, Permitir Reservar, Permitir Cotizar).
- El tilde **Iconnect** del cliente está oculto y en el cliente TEST AGENCIA está destildado, y el usuario opera igual: no es lo que habilita la herramienta. Esto corrige la hipótesis de la parte 1.
- Cliente: **Prioridad Tarifaria** "-1-01-1-11-AE-AJ-XX-". La comisión del cliente está en 0 y el % sale de la solapa **Comisiones** por centro de costo (FD 10%, SPIRIT 20%). Servicio FD Glaciares Gourmet Classic (1230): centro de costo FD, proveedor MARIA TURQUESA (= columna "Catamarán"), ciudad CALAFATE [FTE].
- De las 41 tarifas del servicio, la que muestra iConnect para el 15/11/2026 es la **1097**: prioridad 01, pesos, **Publicar** tildado, Tot. Venta ADU 330.000 / CHD 231.000. Es la única vigente y publicada para esa fecha con una prioridad de la lista del cliente.
- Textgen del servicio: **NOMBRE SERVICIO WEB** = título del detalle ("GLACIARES GOURMET CABINA CLASSIC"); **ITINERARIO EXCURSION** = "Detalle de la Actividad". La solapa **Observaciones** = "Detalle del servicio" del carrito. **ServicioExtra** = adicionales, pero los precios no coinciden con la web (Box lunch 36.199 en iTraffic y 80.000 en la web; a revisar).

## Archivos, tablas y objetos relevantes
- Softur.Serenity: `Modules/E_Ventas/Contacto`, `Modules/A_Maestros/Agencia`, `Modules/A_Maestros/Servicio`, `B_Tarifas/Cost_ser` (servicio `B_Tarifas/Cost_ser/List`), `ScriptsBD/Func/fsp_PrioridadesAgencia.sql`. El código de `iServiciosMuelleWeb` le pasa `@cod_agcia` a `@listaprecio`, y en el repo `fsp_PrioridadesAgencia` no devuelve nada para un código de 5 dígitos, pero en la práctica se aplica la prioridad del cliente: la base de Marpatag puede tener otra versión `[hipótesis]`.

## Cambios hechos
Ninguno en iTraffic (sólo lectura; los diálogos se cerraron sin guardar). En iConnect se cerró el presupuesto de prueba 014358 con "Salir presupuesto".

## Errores y cómo se resolvieron
- Las capturas del navegador integrado tienen tope de 800 px. Solución: la usuaria pasó la ventana de Claude al monitor de 1920×1080, maximizada y con el panel del navegador ampliado, y se capturó la pantalla real con `CopyFromScreen` (con `SetProcessDPIAware`) desde `powershell.exe` 5.1. El recorte de la página quedó en x=1, y=155, 1917×787; viewport 1534×630 CSS con DPR 1,25 (screenshot ×2,397 = px reales). Hay que mantener Claude adelante y no usar la PC mientras se captura.
- `R` también choca con un alias (Invoke-History): las funciones se llaman `Ref`, `Sec`, `Sub`, `Par`, `Add`, `Esc`.
- Las referencias con keepNext dejaban páginas casi vacías: sólo la imagen y su epígrafe llevan keepNext.
- El PDF de ejemplo se lee renderizándolo con `renderpdf.ps1` (Windows.Data.Pdf); la herramienta Read no puede porque no hay pdftoppm.

## Pendientes
- [ ] Completar: ingreso, alta y recuperación de clave; Finalizar reserva y mail; captura de una reserva OB en iTraffic; Volver a cargar reserva; estados (DC); Mis datos — usuaria.
- [ ] Revisar con desarrollo: totales del carrito, precios de adicionales vs ServicioExtra, `@listaprecio` en `iServiciosMuelleWeb`, dónde se usan las imágenes del servicio.

## Cómo validar
Abrir el Word y comparar cada referencia con iConnect e iTraffic (usuario TEST, servicio 1230, tarifa 1097, cliente 11180, contacto 7777).

## Datos que pueden quedar viejos
Disponibilidad (109 lugares el 15/11), tarifas y comisiones del cliente de prueba al 13/11/2026.
