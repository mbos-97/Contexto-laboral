# Movimientos internos y móviles fuera de servicio — Cuenca del Plata

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** No aplica

## Objetivo
Analizar el pedido del cliente de registrar sus movimientos internos (banco, Foz, Ciudad del Este, invitados, Green House, propiedades, taller) y los móviles fuera de servicio.

## Estado final
Análisis entregado a la usuaria; sin documento. Falta su decisión y la consulta al cliente.

## Decisiones y por qué
- Propuesta de la usuaria: cargar un file por cada salida para que Operaciones designe el vehículo y haga un planning. `[decisión]`
- Se recomendó: cliente "Cuenca del Plata Interno" con un tipo de reserva interno; que Operaciones cargue el file porque las salidas son de último momento; un producto "Movimiento interno" con el motivo; y un file "Móvil fuera de servicio". Falta confirmar si los movimientos sólo se registran o también se costean por unidad. `[hipótesis]`
- El planning exige ítems de reserva: sin ellos no se guarda. `[código]`
- Con estado `A`, el planning genera `autoriza` sin un filtro de costo mayor a 0 en ese SP: una salida interna no debería usar ese estado salvo que haya algo que pagar. No se probó. `[código]`
- No se encontró un estado "fuera de servicio" ni una validación de superposición de un vehículo en el planning (`BloqueoEndpoint`, `BloqueoRepository`). El planning tiene una sola fecha, con hora desde y hasta: varios días requieren un planning por día. Los estados salen del parámetro `ESVH`, configurable. `[código]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity (`git pull` previo): `Softur.Serene.Web/Modules/J_Receptivo/Bloqueo/` (`BloqueoEndpoint.cs` línea 29, `BloqueoForm.cs`, `BloqueoRow.cs`, `ParamEstadoLoockupScript.cs`), `iFichaopern_BloqueoAfterSave.sql`. Tablas: `bloqueo`, `det_rva`, `autoriza`, `parame`.

## Cambios hechos
No aplica.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Sin validación de superposición, dos planning pueden tomar el mismo móvil a la misma hora si la búsqueda hecha no omitió otra validación; conviene probarlo. `[hipótesis]`

## Pendientes
- [ ] Probar en una base de prueba una salida interna con costo 0 y un móvil fuera de servicio — Softur.
- [ ] Consultar al cliente si los movimientos se costean por unidad — usuaria.

## Cómo validar
1. En una base de prueba: file interno, ítem, planning sin costo; verificar que no genere autorización y que el móvil figure ocupado.

## Datos que pueden quedar viejos
No aplica.
