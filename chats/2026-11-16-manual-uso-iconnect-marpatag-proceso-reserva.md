# Manual iConnect Marpatag — correcciones de la usuaria y proceso de reserva

- **Fecha:** 2026-11-16
- **Proyecto / cliente:** Marpatag — iConnect
- **Actualiza a:** [2026-11-13-manual-uso-iconnect-marpatag-parte-4.md](2026-11-13-manual-uso-iconnect-marpatag-parte-4.md)

## Objetivo
Retomar el Word que la usuaria corrigió (con ajustes entre paréntesis) y sumar el proceso de Finalizar reserva a partir de las capturas que fue pasando.

## Estado final
Word editado **sobre la versión de la usuaria** (no se regeneró): `Entregables/Manual de uso iConnect - Venta web B2B - Marpatag (marca Softur).docx` + PDF, 26 páginas. Cambios:
- Sus ajustes: "Enviar factura no aplica al módulo iConnect"; sin la marca ni el texto de Comisión 0 (sólo la comisión por centro de costo); sin la config en Tipo de reserva; encabezado con fondo **#003865**; la categoría del cupo tiene que coincidir con la de la tarifa; sin el párrafo de la vista previa de la imagen. Epígrafe para la captura que agregó (reserva OB1802, Tipo Reserva WEB B2B [TPOB]). `[decisión]`
- iTraffic → **iTRAFFIC** en todo el texto. `[decisión]`
- Sección 07, "Finalizar reserva": paso 1 de datos de pasajeros, con la captura marcada (primer pasajero con campos obligatorios, el resto opcionales; según los servicios se piden datos de vuelos y de alojamiento); paso 2 con Información importante para nosotros (se guarda en la solapa **Observaciones** de la reserva y se ve en la ficha operativa), condiciones de compra y Confirmar; "Reserva confirmada" = abre el detalle de la reserva. `[datos]`
- Sección 08: **Cancelaciones**: sólo los servicios principales (no los adicionales) y hasta 1 día antes de la prestación. Liquidación y Estado de cuenta "generan el PDF" (en el navegador integrado se descarga). `[datos]`

## Errores y cómo se resolvieron
- Las imágenes pegadas en el chat después de la primera no llegan como archivo: no se pueden insertar. Quedaron en el Word marcas rojas "[Insertar acá la captura…]".
- XmlDocument: `SetAttribute('space', ns-xml, …)` escribe `d5p1:space` con un xmlns inválido y Word no abre el archivo. Hay que usar `CreateAttribute('xml','space',…)` o corregirlo con regex. Además, `SetAttribute` con namespace devuelve un string que contamina la salida de las funciones: va con `[void]`.
- `-ne` / `-eq` de PowerShell no distinguen mayúsculas: para comparar "iTraffic" con "iTRAFFIC" hay que usar `-cne`.
- `$s` pisa `$S` (otra vez): en los scripts no usar `$s` si existe `$S`.

## Actualización (mismo día)
La usuaria guardó las capturas en `Downloads` y se insertaron marcadas: resto de los pasajeros y Continuar, paso 2, solapa Observaciones de la reserva en iTRAFFIC y reserva confirmada (FD5904, con pasajero, vendedor y cuenta bancaria ocultos). El manual quedó en 28 páginas, con 36 capturas. Para recibir capturas hay que pedir que las guarde como archivo: las pegadas en el chat no llegan. `[datos]`

## Actualización 2 (mismo día)
Se sumaron el aviso "Su reserva ha sido realizada correctamente" con el número **OB1882** (el prefijo OB se confirma; FD5904 era otro caso), el **botón Cancelar** en el detalle de la reserva (junto al estado PC) y el **correo de Reserva creada**: Mail From reservas@ de Marpatag con copia oculta, **Mail To = correo del usuario logueado**, asunto "Cruceros Marpatag - Reserva creada - OBxxxx", y un cuerpo con enlace a la liquidación y a las cuentas bancarias. Manual: 30 páginas, 39 capturas. Se ocultaron el vendedor, el documento, la cuenta bancaria y el correo del usuario. `[datos]`
- Aparecieron `w:ins` de "Microsoft Word" (17:42) por editar mientras el archivo de OneDrive estaba abierto o sincronizando: se limpiaron. Antes de editar, verificar que no haya revisiones (`Revisions.Count`) y pedirle a la usuaria que cierre el Word.

- Índice con hipervínculos: cada línea de la tabla de contenido va envuelta en `<w:hyperlink w:anchor="secNN">` hacia los marcadores `sec01`…`sec11` de los títulos. En Word se usa con Ctrl+clic y en el PDF con clic. `[decisión]`

## Actualización 3 (mismo día)
- Liquidación detallada (RES1) y Estado de cuenta (FSALDRVA) de la reserva 136174: las URL son **públicas** y se bajan sin sesión con `Invoke-WebRequest` (en el navegador integrado disparan una descarga). Se insertaron en la sección 07 como capturas marcadas, ocultando el CUIT/DNI y la dirección del cliente, el vendedor y el pasajero. `[datos]`
- Se quitó la sección **Mis datos** (formulario de la agencia), su entrada del índice y su pendiente. Las secciones quedan 01–10. `[decisión]`
- **iTRAFFIC** e **iCONNECT** siempre en mayúsculas, también en el nombre de archivo: `Manual de uso iCONNECT - Venta web B2B - Marpatag (marca Softur).docx/.pdf`. La config `ReservaIconnectOB` conserva su nombre real. `[decisión]`
- De nuevo `$e` pisó `$E`. Antes de editar, chequear que no haya un `WINWORD` abierto con el manual.

## Actualización 4 (mismo día)
- Pantallas públicas de iCONNECT capturadas con **Edge headless sin sesión** (no se toca la sesión del navegador integrado): ingreso (`/`), recuperar contraseña (modal `#recuperarModal` dentro del login, mostrado con CSS sobre una copia local del HTML con `<base href>`) y registro (`/register`, HTML sin scripts y sin límite de alto; formulario "Registrarse en Marpatag" con usuarios solicitados y botón Enviar). Van al comienzo de la sección 03, "Ingreso e inicio". `[datos]`
- Liquidación y estado de cuenta: quedan sólo la imagen y el texto, sin recuadros ni referencias (pedido de la usuaria). `[decisión]`
- Manual: 31 páginas, 42 capturas. "Marpatag da de alta el cliente y los contactos" tras el registro es una suposición, sin verificar. `[hipótesis]`

## Pendientes
- [ ] Confirmar qué pasa con la solicitud de registro (quién la recibe y cómo se da de alta) — usuaria.
- [ ] Qué significan los estados de la reserva (PC, LI, FI) y del servicio (DC) — usuaria.
- [ ] La reserva real FD5904 salió con prefijo **FD**, no OB: confirmar de qué depende el prefijo.
- [ ] Liquidación (RES1) y Estado de cuenta (FSALDRVA) de la reserva 136174: los enlaces descargan el PDF; hacen falta los archivos para documentarlos.
