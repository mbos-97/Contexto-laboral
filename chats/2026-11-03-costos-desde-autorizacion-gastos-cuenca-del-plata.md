# Costos desde la autorización de pago para gastos — Cuenca del Plata

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-30-proceso-por-sector-v2-cuenca-del-plata-lavadero-parte-2.md](2026-10-30-proceso-por-sector-v2-cuenca-del-plata-lavadero-parte-2.md) (alternativa, sin decidir)

## Objetivo
Analizar la sugerencia de un colega: una reserva por tipo de gasto y por mes, con los costos generados a partir de la autorización de pago de una "letra de reserva".

## Estado final
Análisis entregado; sin cambios en documentos. Falta la decisión de la usuaria.

## Decisiones y por qué
- iTraffic ya tiene la base: con `LRECOSTEOXAUTORIZA = .T.`, al guardar una autorización (`iAutoriza_AfterSave`) corre `idet_rva_UpdatexAutoriza`, que por cada reserva imputada deja un ítem de ajuste (servicio de `SERVCOSTOAUTORIZA`, categoría `COSTEOAUT`) con la diferencia entre lo imputado y el costo de ese operador y moneda. Omite reservas con estado `CD` y puede limitarse con `FECOUTMINAJUFROMAUTORIZA`; `AJUSTECOSFROMAUTPREPROD` lo restringe a usuarios de prueba. `[código]`
- La configuración es general: no vi un filtro por tipo o letra de reserva. Encendida sin filtro, una autorización mayor al costo en cualquier file generaría el costo que falta, en contra de la regla de autorizar sólo lo que existe en el file. Se necesitaría ese filtro. `[código]`
- Recomendación: usarlo para gastos (VTV, controlado, gomería, lavadero, insumos), con reserva mensual por tipo; no para movimientos internos, que necesitan ítem y planning para asignar vehículo. `[hipótesis]`
- "Letra de reserva" se interpretó como tipo de reserva (ej. UC); no se confirmó con el colega. `[hipótesis]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity (`git pull` previo): `iAutoriza_AfterSave.sql`, `idet_rva_UpdatexAutoriza.sql`, `idet_rva_UpdatexAutorizabyReserva.sql`, `iFichaopern_BloqueoAfterSave.sql` (inserta `autoriza` e `imputaci`, con `Idreserva` y `Centrocost`). Módulo `G_Proveedores/Autoriza`. Tablas: `autoriza`, `imputaci`, `det_rva`, `config`.

## Cambios hechos
No aplica.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- No se verificó la configuración de Cuenca del Plata ni se probó el proceso. `[hipótesis]`
- El SP borra y regenera el ítem de ajuste al recalcular: conviene probarlo con varias autorizaciones sobre la misma reserva mensual. `[hipótesis]`

## Pendientes
- [ ] Decidir si la reserva mensual reemplaza al file diario de Nils — usuaria.
- [ ] Confirmar qué significa "letra de reserva" y los valores de configuración del cliente — usuaria / desarrollo.

## Cómo validar
1. En una base de prueba con la configuración activa: autorización imputada a la reserva mensual; verificar el ítem `COSTEOAUT` y que no afecte a otros tipos de reserva.

## Datos que pueden quedar viejos
No aplica.
