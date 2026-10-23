# Respuesta a cliente: la N/C no disminuyó el ingreso / pedido de "cuenta puente de saldos a imputar"

- **Fecha:** 2026-10-23
- **Proyecto / cliente:** cliente en armado de plan de cuentas (nombre no registrado)
- **Actualiza a:** [2026-10-23-asiento-nota-de-credito-vs-factura-venta-parte-2.md](2026-10-23-asiento-nota-de-credito-vs-factura-venta-parte-2.md)

## Objetivo
Redactar la respuesta al cliente, que ve que una factura generó ingreso (799,10) pero la N/C no lo disminuyó y propone una cuenta puente de "saldos a imputar".

## Estado final
Borrador entregado a la usuaria; falta revisar la reserva puntual del cliente.

## Decisiones y por qué
- Respuesta base: la N/C genera el asiento espejo de la factura con las mismas cuentas, así que disminuye el ingreso; no hace falta una cuenta puente para eso. [código]
- La cuenta puente que pide el cliente es una cuenta de pasivo para créditos de N/C pendientes de aplicar (Debe ingreso / Haber saldos a imputar; luego saldos a imputar contra deudores al aplicar). Se puede contemplar en el plan de cuentas, pero hoy el sistema no la usa en la N/C. [hipótesis]
- Posibles causas de que la N/C no haya bajado el ingreso: contabilización desde la liquidación (la N/C va a la transitoria, y en `iAsiento_CreateFacturaComision` todas las líneas salvo IVA se pasan a la cuenta `CMF` del LIQ), cuentas distintas en el detalle de la N/C, o N/C sin asiento (`config LGENASTOFAC`, error 52114 en reservas CM). [hipótesis]
- Se ofrece al cliente un recorrido de procesos con el asiento de cada uno, porque pidió ver los procesos para definir cuentas. [decisión]

## Archivos, tablas y objetos relevantes
- Ver memorias de N/C del 2026-10-23. Tablas `mov_asto`, `Factura`, `Liq_rva`.

## Cambios hechos
No aplica.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Afirmar "la N/C netea" sin revisar la reserva del cliente, cuando el cliente ve lo contrario.

## Pendientes
- [ ] Revisar los asientos de la reserva informada por el cliente (factura, N/C, LIQ) — usuaria / soporte.
- [ ] Enviar el material de la reunión — usuaria.
- [ ] Evaluar armar el recorrido de procesos con asientos para el plan de cuentas — usuaria.

## Cómo validar
Consultar `mov_asto` de la factura y de la N/C de esa reserva y comparar cuentas y lados.

## Datos que pueden quedar viejos
- Ingreso de la factura informada por el cliente — 799,10 — (foto al 2026-10-23)
