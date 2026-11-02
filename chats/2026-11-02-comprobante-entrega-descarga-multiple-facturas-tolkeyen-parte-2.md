# Comprobante de entrega Tolkeyen: versión final y formato para próximos comprobantes

- **Fecha:** 2026-11-02
- **Proyecto / cliente:** Softur — iTraffic, cliente Tolkeyen
- **Actualiza a:** [2026-11-02-comprobante-entrega-descarga-multiple-facturas-tolkeyen.md](2026-11-02-comprobante-entrega-descarga-multiple-facturas-tolkeyen.md)

## Objetivo
Simplificar el comprobante de entrega y dejar definido el formato para los próximos.

## Estado final
Terminado. Documento de 2 páginas (.docx y .pdf), con el mismo nombre de archivo que la versión anterior, a la que reemplaza.

## Decisiones y por qué
- Se sacan el cuadro "Qué se entrega" y el bloque de conformidad con firmas, y también el ítem del botón individual "Descargar PDF" de "A tener en cuenta". `[decisión]`
- "Cómo se usa" pasa a llamarse "Esquema funcional". `[decisión]`
- El nombre del archivo se informa sólo como se descarga hoy, sin comparar con el pedido ni agregar aclaraciones. `[decisión]`
- Todo comprobante de entrega lleva en la portada, además del título y los datos del cliente, el texto estándar de aceptación. `[decisión]`

## Archivos, tablas y objetos relevantes
- `Entregables/Comprobante de entrega - Descarga multiple de facturas - Tolkeyen (marca Softur).docx` y `.pdf`.
- Texto estándar de portada (encabezado "Comprobante de aceptación de requerimiento"): `[decisión]`

> Estimado Cliente,
>
> Le acercamos el siguiente comprobante de entrega del requerimiento solicitado.
>
> De esta forma usted dará consentimiento sobre haber realizado todas las pruebas necesarias y otorgará la facultad para derivar el proyecto/requerimiento al área administrativa con el fin de cumplimentar los pasos necesarios restantes.
>
> Se dará por aceptada la entrega, ante cualquier diferencia o comentario sobre la instalación deben enviar reporte dentro de los 7 días a administracion@softur.com.ar
>
> Muchas gracias.
> EQUIPO DE SOFTUR

## Cambios hechos
- Se regeneró el .docx y el .pdf sobre los archivos de la versión anterior. Sin cambios en iTraffic ni en Softur.Serenity.

## Errores y cómo se resolvieron
- No aplica.

## Riesgos
- El comprobante ya no menciona que el nombre del PDF difiere de la estructura pedida por el cliente (`nombrecliente_letrafac_sucursal_nro_fac_AAAAMMDDHHSS`); Tolkeyen puede reclamarlo dentro de los 7 días. `[datos]`
- La descarga con el botón sigue sin probarse en pantalla. `[datos]`

## Pendientes
- [ ] Probar la descarga con el botón antes de enviar el comprobante — usuaria.

## Cómo validar
1. Abrir el PDF: página 1 con título, datos del cliente y texto de aceptación; página 2 con 01 Esquema funcional, 02 Nombre del archivo y 03 A tener en cuenta (3 ítems).

## Datos que pueden quedar viejos
- Fecha del comprobante — 02/11/2026 — (foto al 2026-11-02)
