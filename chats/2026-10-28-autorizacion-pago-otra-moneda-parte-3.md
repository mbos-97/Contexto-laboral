# Autorización de pago en otra moneda (parte 3): costo y cambio OK, la reserva sigue sin aparecer

**Fecha:** 2026-10-28

## Objetivo

Seguir con [parte 2](2026-10-28-autorizacion-pago-otra-moneda-parte-2.md): el ítem está costeado y el tipo de cambio cargado, pero la autorización no trae la reserva.

## Estado final

Quedan como causas los filtros de la ventana de selección y del SP. Se pasó un checklist y consultas. Sin acceso a la base del cliente. `[código]`

## Decisiones y por qué

No aplica.

## Archivos, tablas y objetos relevantes

- Ventana de selección `E_Ventas/Reserva/LSALDPROV_ForOPA_FPP_Itraffic/LSALDPROV_ForOPA_FPPGrid.ts`: filtros Tipo, Fecha Reserva, Fecha Salida, Fecha Vencimiento, Fecha Servicio y **Rva**. `[código]`
- SP `iLSALDPROV_ForOPA_FPP_Itraffic.sql` `[código]`:
  - Config **`TIENETOPXFEC_SAL = .T.`** (líneas ~273-300): si no se busca por reserva, limita a reservas con fecha de reserva de los **últimos 7 días** y salida desde **hoy − 30**. Una reserva más vieja no aparece si no se escribe su número en "Rva".
  - Operador: `det_rva.cod_oper` tiene que ser igual al operador de la autorización.
  - Pendiente: costo en la moneda del ítem − autorizaciones previas **en esa moneda**. Con `LFILTRASALDOPROV` se oculta si es ≤ 0,50; con `NOIMPUTASALDOMENORACERO`, si es ≤ 0.
  - `LIMPICASALDADASUNAMONEDA = .T.` borra las reservas saldadas en una moneda (`fsp_CostoSaldadoenunaMoneda`).
  - Filtro por pasajero y por circuito (`**CIRC `) si se usan.
  - `CCPCONPLANNING`: con planning, exige que el ítem esté en el planning.

## Cambios hechos

No aplica.

## Errores y cómo se resolvieron

No aplica.

## Riesgos

No aplica.

## Pendientes

- Resultado del checklist y de las consultas.

## Cómo validar

```sql
select r.rva, r.fec_rva, r.fec_sal, d.cod_oper, o.nombre, d.cod_moneda, d.costol from reserva r join det_rva d on d.idreserva=r.idreserva left join operador o on o.cod_oper=d.cod_oper where r.rva='<RVA>'
select a.idautoriza, a.fecha, a.moneda, a.cod_oper, i.importe from imputaci i join autoriza a on a.idautoriza=i.idautoriza join reserva r on r.idreserva=i.idreserva where r.rva='<RVA>'
select Variable, Valor from Config where Variable in ('TIENETOPXFEC_SAL','LIMPICASALDADASUNAMONEDA','LFILTRASALDOPROV','NOIMPUTASALDOMENORACERO','CCPCONPLANNING','LNOFILTRAOPERRVA')
```

## Datos que pueden quedar viejos

Código al 2026-10-28.
