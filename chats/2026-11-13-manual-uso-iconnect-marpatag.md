# Manual de uso de iConnect (venta web B2B de actividades) para Marpatag — base v0.1

- **Fecha:** 2026-11-13
- **Proyecto / cliente:** Marpatag — iConnect (venta web B2B sobre iTraffic)
- **Actualiza a:** No aplica

## Objetivo
Armar la base del manual de uso de la herramienta de venta web B2B de Marpatag (iConnect), que toma el contenido de iTraffic y tiene la parte estética fija.

## Estado final
Base entregada: `Entregables/Manual de uso iConnect - Venta web B2B - Marpatag (marca Softur).docx` (+ PDF de control), 21 páginas, marca Softur, 17 capturas con referencias (letra negra = sale de iTraffic, número naranja = fijo de la herramienta o acción del usuario). Secciones: introducción, ingreso, inicio y navegación, búsqueda, resultados, detalle, carrito/presupuesto, Mi panel y reservas, Mis datos, qué se carga en iTraffic, configs, pendientes. `[decisión]`

## Qué se relevó
- iConnect de Marpatag: `https://marpatag.itraffic.com.ar/iTraffic_Marpatag.iConnect/` (usuario de prueba TEST, lo logueó la usuaria). Pantallas: inicio (`/`), resultados (`/servicesra`), detalle (`/servicera?id=`), carrito (`/cartlist`), Mi panel (`/my-panel`), reservas (`/bookings`), Mis datos (`/settings`). `[datos]`
- Al añadir una actividad al carrito se crea un presupuesto en iTraffic (quedó activo el 014358 del usuario TEST, ARS 653.728,50). No se tocó **Finalizar reserva**. `[datos]`
- Inconsistencias vistas: neto + IVA (653.728,50) ≠ "Total a pagar" del carrito (593.999,99); disponibilidad 115 en el listado y 113 en el detalle; nombre distinto entre listado y detalle; textos "Mi Datos", "Elejí una tipo de fecha", "Catamaran". `[datos]`

## Qué alimenta iConnect (código)
- Búsqueda de actividades: SP `iServiciosMuelleWeb`. Salidas = cupos de servicio (`bloserv`, `con_hab` > 0, disponibilidad = cupo − vendido) o servicios con `confirmacionauto = 1`; columna "Catamarán" = `provedor.nombre` del servicio; nombre = `servicio.descrip`. Ventana de búsqueda: 1 día, o 15 con `FECHAMUELLEMASDIAS`; `SEARCH_ICONNECT_05045` = búsqueda propia de Marpatag. `[código]`
- Tarifas: `json_TarifaMuelleweb` sobre `cost_ser` — vigente para la fecha del servicio y para hoy (`vta_desde`/`vta_hasta`), `Publicar = 1`, prioridad del parámetro `PRTS` ("Precio muelle", retorno MU) o la lista de precios del cliente; precio = venta + IVA + IVA tasa 2 por ADU/CHD/INF; `MOSTRAR_MONEDA_ISO_ICONNECT` muestra ARS/USD. `[código]`
- Adicionales: `json_ExtrasMuelleWeb` (tabla `ServicioExtra` → tarifa `cost_ser` de otro servicio). Imágenes: `json_ImagenesServicios` (`servicio.imagenservicio` 1 a 5). `[código]`
- Al llamar a `json_TarifaMuelleweb`, `iServiciosMuelleWeb` le pasa `@cod_agcia` en el parámetro `@listaprecio` (la lista de precios del cliente se calcula pero no se usa). Posible error, a confirmar con desarrollo. `[hipótesis]`
- Reserva: `Reserva_PostConvertToBookingCMS` con `@esIconnect = 1` y config `ReservaIconnectOB` → tipo `TPOB`, prefijo `OB`. Mails: `Emails_Create` con remitente `MAILFROM_ICONNECT`; plantilla `MailCreateReserva_05045` (link a cuentas bancarias `nosotros.html`). Mi panel: `Reserva_ListSmart` (`ALLRVAS_ICONNECT_MYPANEL`, `RVASICONNECTLIST`). Agencias por usuario: `Agencia_ListTraffic` (`LIMITAAGTICONNECT`, `FILTERCOD_AGCIAICONNECT`, `contacto.usuarioweb`). Cliente: tilde `Agencia.Iconnect`. El código de la app iConnect no está en Serenity. `[código]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity, `Softur.Serene/Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/`: `Sp/iServiciosMuelleWeb.sql`, `Func/json_TarifaMuelleweb.sql`, `Func/json_ExtrasMuelleWeb.sql`, `Func/json_ImagenesServicios.sql`, `Sp/Reserva_PostConvertToBookingCMS.sql`, `Sp/Emails_Create.sql`, `Sp/MailCreateReserva_05045.sql`, `Sp/Reserva_ListSmart.sql`, `Sp/Agencia_ListTraffic.sql`; migración `DefaultDB_20231209_114100_IconnectInicial.cs`; `Modules/A_Maestros/Agencia/AgenciaForm.generated.cs` (campo `Iconnect`).
- Tablas: `servicio`, `cost_ser`, `bloserv`, `provedor`, `catego`, `ServicioExtra`, `CupoReservado`, `parame` (PRTS, STSC), `config`, `agencia`, `contacto`.

## Cambios hechos
Ninguno en el sistema. Queda el presupuesto de prueba 014358 activo en el usuario TEST de iConnect.

## Errores y cómo se resolvieron
- En PowerShell, la función `H` chocó con el alias de Get-History y `A` quedó sin definir en una línea; se renombraron (`Sec`, `Sub`, `Par`, `Add`, `Esc`).
- Arrays de un solo elemento se aplanan en PowerShell (`@(@(...))`): se envuelven con `,$x`.
- Los números de página del índice salían en otra fuente: se agregó `\* MERGEFORMAT` al PAGEREF.
- Las capturas del navegador integrado salen a 800×392; se escalaron 2x para el Word.

## Pendientes
- [ ] Completar: capturas de ingreso, recuperación de clave y alta; pasos de Finalizar reserva y mail; listado con reservas; si Mis datos actualiza el cliente; origen de la comisión del 10% y del texto "Detalle de la actividad" — usuaria.
- [ ] Revisar con desarrollo los totales del carrito, la diferencia de disponibilidad y el parámetro `@listaprecio` de `iServiciosMuelleWeb` — usuaria.
- [ ] Definir con la usuaria si el manual va con marca Softur o de Marpatag, y si se separa en manual de agencia y manual de carga.

## Cómo validar
Abrir el Word en `Entregables` y comparar las capturas con iConnect logueado con un usuario de agencia.

## Datos que pueden quedar viejos
- Actividades vistas el 13/11/2026: Full day Glaciares Gourmet (María Turquesa, ARS) y El Espíritu de los Glaciares (Santa Cruz, USD); ciudad origen Calafate.
