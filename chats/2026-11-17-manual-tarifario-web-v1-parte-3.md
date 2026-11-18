# Manual Tarifario Web v1: secciones Paquetes y Hoteles

- **Fecha:** 2026-11-17
- **Actualiza a:** [2026-11-17-manual-tarifario-web-v1-parte-2.md](2026-11-17-manual-tarifario-web-v1-parte-2.md)

## Estado final
La usuaria pidió frenar y dejar el documento como estaba. Versión vigente: `Entregables/Manual de uso - Tarifario Web v1 (marca Softur).docx` + PDF, 15 páginas. Tiene las secciones 09 Paquetes, 10 Hoteles y 11 Control final, esta última en una página aparte.

## Hallazgos `[datos]`
- **Paquetes** (menú → `/servicios/`, pantalla "Paquete de Servicio", formulario `Type=7`): muestra los servicios con Tipo de Servicio **SERVICIO PAQUETE [SP]** (`tip_serv`). Ejemplo: el servicio 12186 (tipo SP) y el 12178 (tipo E1) tienen la misma Descripción y cada uno aparece en su sección. Las tarjetas y la ventana "Ver tarifas" funcionan igual que en Excursiones.
- **Hoteles** (`/hoteles/`): filtros País, Ciudad, Hotel, Categoría y Ordenar por estrellas. Con el usuario de prueba (cliente con `Listaprecio -BK-DU-PQ-PU-RR-TE-PA-`) devuelve `NO_RATES` en Ushuaia y Calafate, y el combo Hotel queda vacío, aunque `B_Tarifas/Costohtl` tiene 375 tarifas con Publicar, venta y estadía vigentes, varias en prioridad RR. Falta saber qué otra condición pide el PriceList (¿precios en 0?). En el manual figura como "Pendiente de validar".

## Softur.Serenity consultado
- `Web/Modules/L_Configuraciones/Tip_serv` (servicio `Tip_serv/List`), `Web/Modules/B_Tarifas/Costohtl` (servicio `Costohtl/List`), `Model/Modules/D_Paquetes/Entities/PaqueteRow.generated.cs` (imágenes `IMAGENPAQUETEs`; no se ven en el tarifario), `ProvedorRow` (Imagen1-8 del hotel; sin verificar si las usa el tarifario).

## Pendientes
- [ ] Hoteles en el Tarifario Web: confirmar con desarrollo por qué devuelve NO_RATES y relevar resultados, imágenes y tamaños.
