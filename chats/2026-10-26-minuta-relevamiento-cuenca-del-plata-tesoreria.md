# Minuta de relevamiento Cuenca del Plata: sector Tesorería

- **Fecha:** 2026-10-26
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** No aplica (complementa [2026-10-15-circuito-operativo-itraffic-cuenca-del-plata-parte-2.md](2026-10-15-circuito-operativo-itraffic-cuenca-del-plata-parte-2.md))

## Objetivo
Pasar a documento con marca Softur la minuta de los temas que se van hablando en las reuniones con Cuenca del Plata. Primera entrega: relevamiento del sector Tesorería. La usuaria va a ir pasando más sectores.

## Estado final
Parcial (documento vivo). `Trabajo/Entregables/Minuta de relevamiento - Cuenca del Plata (marca Softur).docx` (+ `.pdf` de control), 2 páginas: portada con ficha y sección 01 Tesorería.

## Decisiones y por qué
- Un documento único para toda la minuta, con una sección numerada por sector y cada sector en página nueva — porque la usuaria va a ir sumando sectores. `[decisión]`
- Se transcribe lo hablado sin agregar afirmaciones del sistema (no se consultó Softur.Serenity: la minuta describe cómo trabaja el cliente, no lógica del producto). `[decisión]`
- Lo relevado en Tesorería: `[decisión]` (dicho por el cliente)
  - Pagos siempre contra factura, excepto proveedores de Brasil.
  - Insumos: una persona de administración controla y carga las facturas de proveedores (firmadas por quien autorizó la compra); el responsable de Tesorería hace la autorización de pago, la orden de pago y la caja diaria.
  - Servicios: pago de gastos (carga de factura de gastos) y autorizaciones de pago.
  - La solicitud no es una autorización de pago.
  - Reporte de proveedores desactualizado.
  - Conciliación bancaria: hubo pruebas, no se usa al 100 % porque la mayoría de los movimientos son con cheques.
- Objetivos de la semana: que Tesorería pague sólo autorizaciones de pago; generar las devoluciones desde el sistema. `[decisión]`

## Archivos, tablas y objetos relevantes
- Plantilla: paquete OOXML de `Configuracion Facturacion Electronica Uruguay DGI (marca Softur).docx` (estilos, logo, encabezado y pie), sin la captura de DGI (`image2.png`).
- Generador: script de PowerShell en el scratchpad de la sesión (`minuta.ps1`), con helpers `Section`, `Sub`, `Table`, `Callout`, `Item`; Tesorería es la sección 01.
- Softur.Serenity: no se consultó.

## Cambios hechos
- Se creó el .docx y el .pdf en Entregables. Revisado como PNG con `Windows.Data.Pdf`.

## Errores y cómo se resolvieron
- `Expand-Archive` no acepta `.docx` — copiar como `.zip` y descomprimir con `unzip`.
- `powershell.exe -ExecutionPolicy Bypass` lo bloquea el modo automático — correr `powershell.exe -NoProfile -File` sin ese parámetro (alcanzó).
- Viñetas con texto en dos líneas quedaban desalineadas — usar tabulación después de la marca con sangría francesa de 360.

## Riesgos
- En "Servicios" la minuta no nombra responsable; el documento pone "Tesorería". `[hipótesis]`

## Pendientes
- [ ] Sumar los próximos sectores que pase la usuaria — usuaria / IA.
- [ ] Confirmar responsable de los pagos de servicios — usuaria.

## Cómo validar
1. Abrir el PDF: página 1 portada con ficha (sectores relevados: Tesorería); página 2 sección 01 Tesorería con equipo, regla general, circuito, situación detectada y objetivos.

## Datos que pueden quedar viejos
- Objetivos "de esta semana" — semana del 2026-10-26 — (foto al 2026-10-26)
