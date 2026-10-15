# Circuito operativo iTraffic para Cuenca del Plata (con maestros y ficha operativa)

- **Fecha:** 2026-10-15
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** No aplica

## Objetivo
Convertir el documento "Circuito básico sugerido iTRAFFIC" en un documento con marca Softur para compartir con Cuenca del Plata, sumando la carga mínima de maestros (clientes, operadores, servicios y tarifas), la ficha operativa y el equipo responsable de cada etapa.

## Estado final
Terminado. Se entregaron `Trabajo/Entregables/Circuito operativo iTraffic - Cuenca del Plata.docx` y `.pdf` (10 páginas A4).

## Decisiones y por qué
- Estructura en 10 etapas: 01 Carga de maestros, 02 Alta de reserva, 03 Ficha operativa, 04 Generación de cuentas, 05 Cobros, 06 Pagos, 07 Facturación, 08 Facturas de proveedores, 09 Vencimientos, 10 Caja. Las etapas 04–10 respetan el documento base. `[decisión]`
- Responsables (pedido de la usuaria): maestros → Producto + Data entry; reservas → Ventas; ficha operativa → Operaciones. Para 04–10 se puso "Equipo de Administración" como criterio propio; confirmar con el cliente. `[decisión]` / `[hipótesis]`
- Criterio de tarifas (pedido de la usuaria): en la tarifa se carga sólo el precio de venta, una por prioridad de cliente; el costo se define en la ficha operativa. Excepción documentada: los costos extras (peajes, entradas, honorarios de guía) sí conviene cargarlos con costo porque el planning los toma de una tarifa. `[decisión]`
- Se recomienda un operador + prestador genérico "A designar" para vender receptivos sin prestador real (igual que la guía de ficha operativa). `[decisión]`
- Sin capturas de pantalla: no había capturas con datos de prueba disponibles. `[decisión]`

## Archivos, tablas y objetos relevantes
Softur.Serenity consultado (sólo lectura, `git pull` previo), en `Softur.Serene/Softur.Serene.Web/Modules`: `[código]`
- `A_Maestros/Agencia/AgenciaForm.generated.cs` — cliente: "Prioridad Tarifas" (`Listaprecio`), "Cuenta deudora" (`Cuenta`), Condición IVA (`TIVA`), CUIT, Días venc., pestañas Vencimientos (`Clicob`), Límites de Compra, Comisiones; marcas de Estadísticas (Minorista, Receptivo, OTA, DMC, Pasajero Directo, Tour Operador), Cuenta Corriente / Prepago.
- `E_Ventas/Reserva/ReservaDialog.ts` — con `IT_SERVAUTOPRIO` (default true) la reserva filtra tarifas por `Prioridad in Listaprecio`; `Listaprecio` admite varias separadas por "-"; vacía = no filtra.
- `A_Maestros/Operador/OperadorForm.generated.cs` — Tipo (`TIPR`), cuentas contables (`Ctacte`, `Cta_anticipo`, `Nro_cuenta`), Días Vencimiento, Forma Pago, pestañas Política Pagos / Política de Cancelación.
- `A_Maestros/Provedor/ProvedorForm.generated.cs` — el prestador tiene campo Operador.
- `A_Maestros/Servicio/ServicioForm.generated.cs` — Proveedor, Tipo de Servicio, "Tipo de Costeo" (`Pago`, parámetro `FPSE`: Precio por Día / Precio Total / Precio por Semana).
- `Softur.Serene.Model/Modules/L_Configuraciones/Entities/Tip_servRow.generated.cs` — tipo de servicio con "Precio por Reserva" (`Paga_rva`). Menú Configuraciones > Tipo Servicios.
- `B_Tarifas/Cost_ser/Cost_serForm.generated.cs` — tarifa: vigencia, venta desde/hasta, Categoría, Prioridad, Moneda / Moneda Venta, "Precios por Rango de Pax" (Pax desde/hasta), "Costea CHD como Adulto".
- `J_Receptivo/Vehiculo`, `J_Receptivo/Chofer` — vehículo (Capacidad, Tipo, Es propio, Proveedor, vigencia); chofer (Código, Nombre, Libreta, Cargo).
- `J_Receptivo/Bloqueo/BloqueoDialog.ts` y `BloqueoForm.cs` — planning: vehículo (trae su prestador y filtra las tarifas de costo por prestador y fecha), chofer, horas, estado (parámetro `ESVH`), servicio de costo, costo total, base pax, adicionales.
- `J_Receptivo/Bloqueoadic/BloqueoadicEditorDialog.ts` — costos extras del planning: servicio adicional, servicio al que aplica, base pax, costo adulto/menor/infante, moneda.
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/iFichaopern_BloqueoAfterSave.sql` — al guardar el planning: genera `autoriza` (autorización de pago) por planning y por adicional; reparte el costo `bloqueo.Costo / basepaxplan * det_rva.Basepax`; con config `LUPDCODOPERVEHICULO` asigna a los servicios el operador del prestador del vehículo; actualiza costeo de la reserva.
- `J_Receptivo/FichaOperativa/FichaOperativaEndpoint.cs` — guía por prestador (`cod_guiaprov`) y costo editable por ítem (`det_rva.costo`).

## Cambios hechos
- Se creó el .docx (OOXML armado desde PowerShell, estilos y logo reutilizados de `Ficha operativa - Guia rapida.docx`) y el PDF exportado con Word. No se modificó el documento base ni el repo Softur.Serenity.

## Errores y cómo se resolvieron
- El .docx del Itinerario dinámico estaba bloqueado por otro proceso — se usó como molde la guía de Ficha operativa en `Trabajo/`.
- La ficha operativa quedaba con una hoja casi vacía — se forzó salto de página antes de 03 y se quitó el de 04.

## Riesgos
- El reparto automático del costo al operador del vehículo depende de la config `LUPDCODOPERVEHICULO`; en el documento figura como "opción que se define en la implementación". `[código]`
- Que el honorario del guía se cargue como costo extra es una recomendación de trabajo, no un comportamiento verificado del sistema. `[hipótesis]`
- Los estados del planning vienen de datos (`ESVH`); el documento sólo nombra "Cerrado". `[código]`
- El ejemplo de tarifas (City tour, prioridades 01/02/03, importes) es ilustrativo. `[decisión]`

## Pendientes
- [ ] Confirmar con Cuenca del Plata los responsables de las etapas 04–10 y el referente de cada equipo — usuaria.
- [ ] Definir con el cliente la tabla de prioridades de clientes — usuaria / cliente.
- [ ] Decidir si se activa `LUPDCODOPERVEHICULO` para choferes que son operadores — implementación.

## Cómo validar
1. Abrir el PDF: 10 páginas; portada con tabla de 10 etapas y responsables; 01 en página 2, 02 en página 6, 03 en página 7.
2. En una base de prueba: crear un cliente con prioridad, una tarifa con esa prioridad, una reserva, y en la ficha operativa un planning con costo total; verificar el reparto por pasajeros y la autorización de pago.

## Datos que pueden quedar viejos
- Nombres de campos y menús — según el código al 2026-10-15
- Valores de `FPSE` (Precio por Día / Total / por Semana) — según los scripts de datos por defecto al 2026-10-15
