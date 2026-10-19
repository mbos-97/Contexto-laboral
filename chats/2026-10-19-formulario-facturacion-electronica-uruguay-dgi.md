# Formulario de configuración de facturación electrónica Uruguay (DGI) con marca Softur

- **Fecha:** 2026-10-19
- **Proyecto / cliente:** Softur — iTraffic, clientes de Uruguay (formulario genérico, sin cliente puntual)
- **Actualiza a:** No aplica

## Objetivo
Armar un Word con marca Softur, con tablas para que el cliente complete los datos necesarios para configurar la facturación electrónica (CFE) ante DGI Uruguay en iTraffic.

## Estado final
Terminado. `Trabajo/Entregables/Configuracion Facturacion Electronica Uruguay DGI (marca Softur).docx` (+ `.pdf` de control), 4 páginas.

## Decisiones y por qué
- Datos que completa el cliente (definidos por la usuaria): RUC, razón social, domicilio fiscal, departamento, ciudad, correo, sucursal, certificado .pfx (archivo), clave del .pfx, resolución de DGI que aprueba al emisor, URL del comercio declarada ante DGI y un CAE por tipo de comprobante (e-Factura, NC de e-Factura, e-Ticket, NC de e-Ticket). `[decisión]`
- CAE = rango de documentos habilitados; se gestiona en https://servicios.dgi.gub.uy/serviciosenlinea › Constancias › "Autorización Impresión Documentación - Solicitud". `[decisión]`
- La tabla de CAE pide además serie, desde/hasta y vencimiento, y trae el código de tipo de CFE precargado (e-Ticket 101, NC e-Ticket 102, e-Factura 111, NC e-Factura 112). `[hipótesis]` (códigos estándar DGI, no verificados en el código de Serenity)
- La clave del .pfx no va en el documento: se marca con un tilde "Enviada por canal separado" y se pide mandarla por otro canal que el archivo. `[decisión]` (criterio de seguridad propuesto en el documento)
- Estructura: 01 Cómo completar · 02 Datos del emisor · 03 Certificado digital · 04 Habilitación DGI · 05 CAE por tipo · 06 Cómo solicitar los CAE (captura del menú Constancias con referencias 1 Solicitud, 2 Consulta de solicitudes, 3 Consulta solicitudes emitidas) · 07 Datos de quien completa + próximos pasos. Campos numerados 1 a 15. `[decisión]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity (sólo lectura, `git pull` previo): búsqueda rápida de la configuración CFE Uruguay. No aparece una pantalla de configuración del emisor UY en el código consultado; sólo `AgenciaRow.generated.cs` (campo `Resolucion` del cliente/agencia), `FacturaRow.generated.cs` (campo `Cae` de la factura) y `IImport_Fac_Prov_UY.sql` (tipos "e-Ticket Nota de Crédito" → NCC en importación de facturas de proveedores). `[código]`
- Captura de referencia: menú "Constancias" de Servicios en línea de DGI (provista por la usuaria), marcada con C# `System.Drawing`.

## Cambios hechos
- Se creó el .docx reutilizando el paquete OOXML de "Propuesta PaxDirect - Marpatag (marca Softur).docx" (estilos, logo, encabezado y pie), con el `document.xml` generado por script de PowerShell y empaquetado con `System.IO.Compression`. PDF exportado con Word por COM y revisado como PNG con `Windows.Data.Pdf`.

## Errores y cómo se resolvieron
- `Get-Item "...\[Content_Types].xml"` no encuentra el archivo (los corchetes son comodines) — usar `-LiteralPath`.
- Un salto de página en un párrafo vacío deja hueco arriba — poner `pageBreakBefore` en el propio título de sección.

## Riesgos
- Los códigos de tipo de CFE precargados y el nombre exacto de "sucursal" (código de establecimiento DGI) conviene validarlos con quien implementa la facturación UY. `[hipótesis]`

## Pendientes
- [ ] Validar con implementación si falta algún dato técnico (ej. usuario/clave de servicios web, ambiente de homologación) — usuaria.

## Cómo validar
1. Abrir el .docx: portada con logo, secciones 01–07, campos 1–15, figura 1 con referencias 1–3.
2. Las celdas blancas son editables en Word.

## Datos que pueden quedar viejos
- Menú de DGI "Constancias" y nombres de las opciones — (foto al 2026-10-19)
