# Relevamiento Marpatag: venta a Amex con dos condiciones comerciales

- **Fecha:** 2026-10-09
- **Proyecto / cliente:** Marpatag (iTRAFFIC)
- **Actualiza a:** No aplica

## Objetivo
Armar un relevamiento funcional en Word para que Marpatag pueda venderle a Amex con dos condiciones: la actual (venta neta, comisión descontada) y una nueva (factura y cobro del 100% al pasajero directo, comisión liquidada a Amex).

## Estado final
Terminado: borrador v1.0 para validación del cliente. Archivo: `Trabajo/Relevamiento_Marpatag_Amex_Condiciones_Comerciales.docx` (7 páginas, fuera de este repo).

## Decisiones y por qué
- Condición 1 = esquema actual: cliente Amex, rack − % comisión (pestaña Comisiones del ABM Cliente). [datos]
- Condición 2: cliente principal Consumidor Final, factura B por el total del file. Si el pasajero pide factura A, el pasajero va como cliente principal. [decisión]
- Amex va como cliente secundario en Condición 2, para estadísticas. [decisión]
- Amex define la condición al comprar, con usuario B2B. [decisión]
- Cobro: link de pago de Marpatag al pasajero, 100% antes del viaje. [decisión]
- Comisión: mismo % por producto ya cargado, sobre la tarifa rack sin impuestos. Se genera un ítem con venta 0, costo = comisión y operador Amex. [decisión]
- Pago a Amex: liquidación mensual, a veces con factura de Amex y a veces sin comprobante. [decisión]
- Reportes: solo los de estadísticas de venta muestran el cliente secundario. Los contables siguen con el cliente principal. [decisión]
- Propuesta de Softur: parámetro en ABM Cliente, campo "Condición comercial" en la reserva y selección obligatoria en B2B. Aplicar el reemplazo de cliente en estadísticas solo en Condición 2. [hipótesis] (pendiente de validar con el cliente)

## Archivos, tablas y objetos relevantes
- ABM Clientes > pestaña Comisiones (Idagencia, cod_agencia, centro de costo, % comisión, vigencia, país, ciudad).
- Centros de costo de Amex vistos: ADM'STA CRUZ, CHARTER, FD, SPIRIT, SIN COMISION. [datos]
- Módulos: Reservas, Web B2B, Facturación, Cuentas a pagar/Operadores, Reportes de estadísticas.

## Cambios hechos
- Se creó el relevamiento en Word (desde HTML, con Word COM).

## Errores y cómo se resolvieron
- No hay Node ni Python en la PC para generar el .docx — se armó en HTML y se convirtió con Word COM (SaveAs2 formato 16), con la imagen embebida (BreakLink).

## Riesgos
- Si el reemplazo por cliente secundario se aplica a todas las reservas, se alteran las estadísticas de otros clientes.
- Doble comisión si en Condición 2 se descuenta del precio y además se genera el ítem.

## Pendientes
- [ ] Validar el relevamiento con Marpatag — comercial Softur.
- [ ] Definir con Marpatag: qué ve Amex en B2B, quién carga los datos fiscales del pasajero, criterio de la liquidación mensual, falta de pago, cancelaciones con gastos, cambio de condición, plataforma del link de pago, IVA de la comisión, moneda.
- [ ] Volumen mensual estimado de la Condición 2: el cliente no lo sabe todavía.

## Cómo validar
Abrir el .docx y revisar las secciones 3 (comparativo y ejemplo), 4 (propuesta) y 7 (puntos a definir) contra lo acordado con el cliente.

## Datos que pueden quedar viejos
- % de comisión en el ABM de Amex: 0% en ADM'STA CRUZ y SIN COMISION, 15% en CHARTER y SPIRIT, 10% en FD — (foto al 2026-10-09)
