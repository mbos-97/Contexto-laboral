# Proceso administrativo contable — Trips South America

- **Fecha:** 2026-11-16
- **Proyecto / cliente:** Softur — implementación iTRAFFIC, cliente Trips South America (TSA)
- **Actualiza a:** No aplica (documento nuevo; toma como modelo `CLIENTES/TSA/Proceso sugerido para implementacion interna.pdf`)

## Objetivo
Armar un documento como "Proceso sugerido para implementación interna" de TSA, con la marca Softur, mostrando el proceso administrativo contable de la carga de reservas con foco en las autorizaciones de pago: reserva → ficha operativa → planning → autorización de pago → factura de proveedor imputada al planning; sin planning, autorización contra la reserva y luego OP.

## Estado final
Terminado. `Trabajo/Entregables/Proceso administrativo contable - Trips South America (marca Softur).docx` (+ `.pdf`), 11 páginas: portada con etapas · mapa del proceso (diagrama) · 01 Alta de reserva · 02 Ficha operativa · 03 Planning · 04 Autorizaciones de pago (comparativo con/sin planning, 4.1 y 4.2, reglas) · 05 Facturas de proveedor (5.1 al planning, 5.2 a la reserva) · 06 Órdenes de pago · 07 Cobros y facturación · 08 Seguimiento y control diario.

## Decisiones y por qué
- Diagrama propio con color por responsable (Arena = Reservas, Tinta = Operaciones, blanco con borde terracota = Administración, naranja = Tesorería), número = sección; tres columnas: cobros, con planning, sin planning. `[decisión]`
- Sin planning: AUT manual → OP → factura de proveedor contra la reserva "cuando llega" (línea punteada). Pedido de la usuaria. `[decisión]`
- Responsables genéricos (Reservas, Operaciones, Administración, Tesorería): no hay relevamiento de personas de TSA. `[hipótesis]`
- Frecuencias de los controles (diaria / semanal) son sugerencia. `[hipótesis]`
- No se incluyó el circuito de anticipos (AUT sin imputar → OP → Reimputación OP) porque no está probado. `[decisión]`
- Portada sólo con logo Softur (no hay logo de TSA en recursos). `[decisión]`

## Archivos, tablas y objetos relevantes (Softur.Serenity, `git pull` previo)
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/iFichaopern_BloqueoAfterSave.sql`: con planning en estado `A` inserta en `autoriza` una AUT por servicio de costo y por adicional (`idbloqueo`, `idbloqueoadic`), sólo si no existe ya (no se regenera si cambia el costo), con observación "Autorizado desde planning PL" + número, e inserta `imputaci`. `[código]`
- `.../Sp/iLSALDPROV_ForOPA_FPP_Itraffic.sql`: `@tipocc` 1 costos vs pagos, 2 costo vs factura, 3 costos vs autorización, 4 factura vs pagos, 5 factura vs autorización, 6 autorización vs pagos, 7 OP vs factura, 11/12 costo no imputado. Con `@rva` = "?nro" (o "?n1,n2") y tipocc 1–3 filtra los ítems del planning (`det_rva2.idbloqueo` / `iddestino`); config `CCPCONPLANNING` agrupa por planning; `TOLERANCIASALDOAUTFPP` (default 0,50). `[código]`
- `.../Sp/iFacProv_AfterSave.sql`: si la observación de la línea (`fac_ing.observ`) empieza con "PL" + número, completa `fac_ing.idbloqueo`; con `LRECOSTEOXFACPROV` y `ajuste_costo` recostea desde la factura. `[código]`
- `Softur.Serene.Web/Modules/G_Proveedores/Autoriza/AutorizaForm.generated.cs`: campos Moneda, Fecha, Operador, Cuenta, Cambio vs Peso, Descrip. `[código]`
- Generador (scratchpad, no persiste): `gen.ps1` + `contenido.ps1` + `Diagrama.cs`, base = paquete de "Proceso de cancelaciones - Cuenca del Plata (marca Softur).docx" sin el logo de Cuenca.

## Cambios hechos
- Se crearon el .docx y el .pdf en Entregables.

## Errores y cómo se resolvieron
- Word decía "archivo corrompido" — `ZipFile.CreateFromDirectory` en PowerShell 5.1 guarda rutas con `\` (y se coló un .txt de inspección) — se arma el zip entrada por entrada con `/`.
- Los .ps1 con tildes en PowerShell 5.1 se leen mal sin BOM — se reescriben en UTF-8 con BOM antes de correr.

## Riesgos
- El menú "Proveedores › Autorización de pago" y la búsqueda "?nro" en la imputación de la factura se infieren del código, no se probaron en pantalla. `[hipótesis]`
- Si TSA no costea en el planning, la sección 03 (reparto de costo por pax) no aplica tal cual. `[hipótesis]`

## Pendientes
- [ ] Validar con TSA responsables por área y frecuencias de control — usuaria.
- [ ] Probar en base de prueba la búsqueda "?nro de planning" al imputar una factura de proveedor — implementación.

## Cómo validar
1. Abrir el PDF: 11 páginas; página 2 con el diagrama de tres columnas y leyenda; sección 04 con tabla comparativa y 4.1/4.2.

## Datos que pueden quedar viejos
No aplica.
