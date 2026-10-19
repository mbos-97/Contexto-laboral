# Propuesta PaxDirect para Marpatag: ajustes y costos

- **Fecha:** 2026-10-19
- **Proyecto / cliente:** Softur — iTraffic, cliente Marpatag (Amex)
- **Actualiza a:** [2026-10-19-propuesta-paxdirect-marpatag-amex.md](2026-10-19-propuesta-paxdirect-marpatag-amex.md)

## Objetivo
Ajustar la propuesta según la revisión de la usuaria y sumar costos y plazos.

## Estado final
Terminado. `Trabajo/Entregables/Propuesta PaxDirect - Marpatag (marca Softur) v2.docx` y `.pdf`, 4 páginas. La v1 quedó sin tocar porque estaba abierta en Word.

## Decisiones y por qué
- Solapa Beneficios Corporativos: sólo "Operador para ítem de beneficio" y la grilla Tipo de producto + % Beneficio. Sin vigencia, país ni ciudad. `[decisión]`
- No hay "Habilita PaxDirect": el cliente que no tiene la solapa cargada no genera nada aunque se marque el tilde en la reserva. `[decisión]`
- Marpatag vende sólo servicios: los ejemplos son "GLACIARES GOURMET" y "ESPIRITU DE LOS GLACIARES" (SE 15% → 3.000 + 1.500 = 4.500). Sin hoteles ni paquetes. `[decisión]`
- Pago a Amex: siempre con factura de Amex. Si no hay factura real, la idea interna es cargar un comprobante X para tener el registro, pero **no se detalla todavía al cliente**. `[decisión]`
- Se sacó la sección "Para validar" (puntos a confirmar) y "Próximos pasos". `[decisión]`
- Nueva sección 06 "Costos y plazos": **USD 1.400**; 60% anticipo (USD 840), 40% contra entrega (USD 560); entrega 60 días. `[decisión]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity: no se consultó código nuevo.

## Cambios hechos
- Maquetas de cliente y detalle de reserva regeneradas; documento v2 en Entregables.

## Errores y cómo se resolvieron
- El .docx estaba abierto en Word — se guardó como v2. Al exportar a PDF por COM, cerrar Word sólo si no quedan documentos abiertos (`$w.Documents.Count -eq 0`) para no cerrar el Word de la usuaria.

## Riesgos
- No se aclara desde cuándo corren los 60 días (aprobación o pago del anticipo) ni si el precio incluye impuestos. `[hipótesis]`

## Pendientes
- [ ] Borrar la v1 cuando la usuaria cierre el Word, si no la necesita — usuaria.
- [ ] Enviar la propuesta a Marpatag — usuaria.

## Cómo validar
1. Abrir el PDF v2: 4 páginas; la sección 06 dice USD 1.400, 60/40, 60 días; la figura 3 muestra el ítem 003 AMEX con costo 4.500.

## Datos que pueden quedar viejos
- Precio de la propuesta — USD 1.400 — (foto al 2026-10-19)
