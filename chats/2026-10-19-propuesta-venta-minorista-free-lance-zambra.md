# Propuesta Venta Minorista Free Lance para Zambra Tours

- **Fecha:** 2026-10-19
- **Proyecto / cliente:** Softur — iTraffic, cliente Zambra Tours
- **Actualiza a:** No aplica (mismo esquema que [2026-10-19-propuesta-paxdirect-marpatag-amex-parte-3.md](2026-10-19-propuesta-paxdirect-marpatag-amex-parte-3.md))

## Objetivo
Armar para Zambra la misma propuesta que PaxDirect, aplicada a la venta minorista hecha por free lance.

## Estado final
Terminado. `Trabajo/Entregables/Propuesta Venta Minorista Free Lance - Zambra Tours (marca Softur).docx` y `.pdf`, 4 páginas.

## Decisiones y por qué
- Nombre del proceso: **Venta Minorista Free Lance**. `[decisión]`
- Cada free lance se carga como **cliente** (y también como operador) con la solapa **Beneficios Corporativos** cargada; la reserva minorista va a nombre del free lance, con el tilde "Cobro y facturación al pasajero"; al guardar se genera el ítem de comisión con el free lance como operador (venta 0, costo = comisión). `[decisión]`
- Tipos de producto para Zambra: eventuales aéreos, eventuales hoteles, eventuales traslados y eventuales paquetes. `[decisión]`
- El tipo de reserva minorista **ya está creado**; también se usan la sucursal y los centros de costo "minorista" del documento anterior. `[decisión]`
- Pago de la comisión: con factura del free lance (sin detallar otras formas). `[decisión]`
- Costos: **USD 400 + IVA**, 50% anticipo (USD 200 + IVA) y 50% contra entrega; **40 días desde el ingreso del anticipo**. `[decisión]` (el "desde el ingreso del anticipo" se tomó igual que en Marpatag `[hipótesis]`)

## Archivos, tablas y objetos relevantes
- Documento previo enviado a Zambra: "Implementación de la Venta Minorista" (Dropbox, PDF de 2 páginas): tipo de reserva, sucursal y centros de costo "minorista"; tickets aéreos en reserva minorista con cliente Consumidor Final y operador BSP; reportes Reserva List / Caja List por tipo de reserva, sucursal o centro de costo; sin facturación entre marcas (misma razón social).
- Softur.Serenity (sólo lectura): `Softur.Serene.Model/Modules/B_Tarifas/Entities/EventualRow.cs` — el eventual tiene `Ts` (tipo de prestación), `Centrocosto`, `Cod_oper`, `Cod_prov`; sirve para distinguir eventuales aéreos/hoteles/traslados/paquetes. `[código]`

## Cambios hechos
- Maquetas nuevas (`z_*.html`) a partir de las de Marpatag: cliente FREE LANCE 01 con 4 tipos de eventual, reserva MN2031 tipo/sucursal MINORISTA, detalle con ítem 004 "COMISION FREE LANCE - VENTA MINORISTA" (5% aéreo, 10% hotel, 10% traslado → 12.000).

## Errores y cómo se resolvieron
- Abrir un PDF con Word por COM se colgó (diálogo de conversión oculto) — se cortó el proceso de Word propio (por hora de inicio, no el de la usuaria) y el PDF se leyó renderizando páginas a PNG con `Windows.Data.Pdf`.

## Riesgos
- En el documento anterior las reservas minoristas con aéreos iban a Consumidor Final; en esta propuesta la reserva va a nombre del free lance. Puede generar dudas en Zambra. `[hipótesis]`
- La forma de identificar cada tipo de eventual (tipo de prestación o centro de costo) no se definió en el documento. `[hipótesis]`

## Pendientes
- [ ] Enviar la propuesta a Zambra — usuaria.

## Cómo validar
1. Abrir el PDF: 4 páginas; portada "Venta Minorista Free Lance"; sección 06 con USD 400 + IVA, 50/50, 40 días.

## Datos que pueden quedar viejos
- Precio — USD 400 + IVA — (foto al 2026-10-19)
