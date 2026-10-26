# Minuta Cuenca del Plata: Cuenca del Plata SaaS como operador de transporte

- **Fecha:** 2026-10-26
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria-parte-3.md](2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria-parte-3.md)

## Objetivo
Sumar al circuito cruzado que Cuenca del Plata SaaS pasa a ser operador de Cuenca del Plata: presta los servicios de transporte y le factura a Cuenca del Plata.

## Estado final
Terminado. 9 páginas. PDF reemplazado; el Word quedó como `Minuta de relevamiento - Cuenca del Plata (marca Softur) v3.docx` porque la v2 y el original estaban abiertos en Word.

## Decisiones y por qué
- Cuenca del Plata SaaS = operador (cuenta corriente de proveedor) de Cuenca del Plata para el transporte; factura a Cuenca del Plata. `[decisión]`
- Armado en iTraffic propuesto (página 3 de la minuta): alta del operador → prestadores y vehículos propios asociados a ese operador → servicios de costo de transporte con prestador de Cuenca del Plata SaaS → planning → factura con número de planning → Proveedores controla y Tesorería paga. `[decisión]`
- Al guardar el planning, la autorización de pago (`autoriza`) del costo del planning sale a nombre del operador del prestador del **servicio de costo** del planning (`bloqueo.cod_serv` → `servicio.cod_prov` → `provedor.cod_oper`); para los adicionales, el del servicio de costo del adicional. Con la config `LUPDCODOPERVEHICULO = .T.` además se pone en los ítems de la reserva (`det_rva.cod_oper`) el operador del prestador del **vehículo**. Por eso tanto los servicios de costo como los vehículos tienen que colgar de prestadores de Cuenca del Plata SaaS. `[código]`
- Nuevo punto a confirmar (07.6): tarifa a la que Cuenca del Plata SaaS factura el transporte, quién la carga y desde qué fecha rige. `[hipótesis]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity (`git pull` previo): `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/iFichaopern_BloqueoAfterSave.sql` — armado de `@tmpbloqueos` (planning y adicionales, con `provedor.cod_oper`), `insert into autoriza` y bloque `LUPDCODOPERVEHICULO`. Tablas: `bloqueo`, `bloqueoadic`, `vehiculo`, `servicio`, `provedor`, `autoriza`, `det_rva`, `config`.
- Generador: `minuta.ps1` (`Sub` acepta `-NewPage`) + `contenido.ps1` en el scratchpad de la sesión.

## Cambios hechos
- Sección 01: subsección "Transporte propio: Cuenca del Plata SaaS como operador" en página propia (callout + tabla de 6 pasos); "Qué necesitamos para el primer día" suma la carga de Cuenca del Plata SaaS; mapa de sectores actualizado; punto 07.6 nuevo.

## Errores y cómo se resolvieron
- La tabla nueva se cortaba entre páginas — la subsección arranca en página nueva (`pageBreakBefore` en el subtítulo).
- Los Word anteriores estaban abiertos — se guardó como v3.

## Riesgos
- Quedan tres Word de la minuta en Entregables (original, v2, v3); el vigente es la v3. `[decisión]`
- Si la config `LUPDCODOPERVEHICULO` no está activa, los ítems de la reserva no toman el operador del vehículo (la autorización de pago igual sale por el servicio de costo). `[código]`

## Pendientes
- [ ] Confirmar tarifa, responsable de carga y fecha de inicio de Cuenca del Plata SaaS — usuaria.
- [ ] Verificar en la base del cliente el valor de `LUPDCODOPERVEHICULO` — implementación.
- [ ] Borrar los Word viejos de la minuta y dejar sólo la v3 — usuaria.

## Cómo validar
1. PDF de 9 páginas: página 3 con la subsección de Cuenca del Plata SaaS y la tabla completa de 6 pasos.
2. En base de prueba: planning con vehículo y servicio de costo de un prestador de Cuenca del Plata SaaS → la autorización de pago sale a ese operador.

## Datos que pueden quedar viejos
No aplica.
