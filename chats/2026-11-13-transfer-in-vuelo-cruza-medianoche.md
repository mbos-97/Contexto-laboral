# Transfer IN con vuelo que cruza la medianoche (iTraffic)

- **Fecha:** 2026-11-13
- **Proyecto / cliente:** iTraffic receptivo (consulta general)
- **Actualiza a:** No aplica

## Objetivo
Definir cómo cargar un TRF IN cuyo vuelo sale 31/12 23:30 y llega 01/01 00:05, para que la Ficha Operativa y el planning de Operaciones lo muestren el 31/12 (el chofer sale 23:30 del 31).

## Estado final
Terminado: respuesta operativa basada en código.

## Decisiones y por qué
- La fecha del servicio (`det_rva.in_`, campo `Fecha` de la Ficha Operativa) es la que manda en Ficha Operativa y planning: cargar el TRF IN con fecha 31/12 y hora 23:30. [código]
- El vuelo se carga como es (fecha 31/12, sale 23:30, llega 00:05). [código]
- La asociación automática vuelo→transfer (`iReserva_AsociarTrfSmart`) calcula la fecha de llegada: si `hora_llega < hora_sale` suma un día a `rvavuelo.fec_desde`, y une el vuelo de llegada con el ítem por `fec_desde calculada = det_rva.in_`. Con el TRF el 31/12 y llegada calculada 01/01, **no lo asocia solo**: hay que asociar el vuelo a mano en la ficha. [código]
- El SP no pisa `vuelo1` / `vuelo2` cuando terminan en `**` (marca de dato manual). [código] Cómo pone la marca la pantalla: [hipótesis], validar en el sistema.
- Config `FECHATEXTUALVUELOFICHA = .T.` hace que se use la fecha de salida tal cual (sin sumar día): resolvería este caso, pero es global para toda la base. [código]
- El planning (`BloqueoRow`) tiene `Fecha`, `Horadesde`, `Horahasta` (texto); cómo se comporta con hora hasta menor a hora desde (23:30 → 00:30) no está verificado. [hipótesis]

## Archivos, tablas y objetos relevantes
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/iReserva_AsociarTrfSmart.sql` (cálculo de fecha de llegada, join `din.fec_desde = b.in_`, flag `FECHATEXTUALVUELOFICHA`).
- `Softur.Serene.Web/Modules/J_Receptivo/FichaOperativa/FichaOperativaRow.cs` (`Fecha`, `Hora`, `Vuelo1`, `Vuelo2`, `Horasal1`, `Horalle1`, `TipoHora`).
- `FichaOperativaRepository.cs` → `UpdateVuelo` (`hora_sale` / `hora_llega`).
- `Softur.Serene.Web/Modules/J_Receptivo/Bloqueo/BloqueoRow.cs` (`Fecha`, `Horadesde`, `Horahasta`).
- Tablas: `det_rva`, `det_rvao`, `rvavuelo`, `config`.

## Cambios hechos
No aplica (consulta).

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Activar `FECHATEXTUALVUELOFICHA` cambia la asociación de todos los vuelos que cruzan medianoche en toda la base.
- Si se reprocesa la asociación y el vuelo manual no quedó marcado, se puede borrar.

## Pendientes
- [ ] Confirmar en pantalla cómo se asocia el vuelo manualmente y que quede protegido (`**`) — usuaria.

## Cómo validar
Cargar en una base de prueba la reserva con TRF IN 31/12 23:30 y el vuelo 31/12 23:30→00:05, abrir la Ficha Operativa del 31/12 y verificar fecha, hora y vuelo; armar el planning y ver la asignación.

## Datos que pueden quedar viejos
- Lógica del SP — foto al 2026-11-13.
