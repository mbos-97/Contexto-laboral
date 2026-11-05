# Minuta comercial: oportunidades con la migración de Traffic a iTraffic

- **Fecha:** 2026-11-05
- **Proyecto / cliente:** Cliente con Traffic (versión anterior, en Fox); nombre pendiente de la usuaria
- **Actualiza a:** No aplica

## Objetivo
Armar una minuta con espíritu comercial para el dueño de la empresa, con las mejoras detectadas en la oficina para vender junto con la migración.

## Estado final
Parcial: documento terminado en 4 páginas, con cliente, dueño, fecha y participantes como datos a completar (resaltados).

## Decisiones y por qué
- Cada oportunidad lleva un estado (Disponible, Se activa, Se adapta, Desarrollo, A definir) — vender sin prometer como listo lo que requiere trabajo. `[decisión]`
- Sin precios: lo que requiera activación o desarrollo se cotiza en una propuesta aparte. `[decisión]`
- No se nombran otros clientes de Softur, salvo Infoterra, que indicó la usuaria. `[decisión]`
- El esquema de tiempos es una primera referencia, tomada de propuestas previas, a confirmar por Softur. `[hipótesis]`

## Qué dice el código y las propuestas previas
- **Omnibees:** en Softur.Serenity sólo figura como tipo de producto en `Parames_PlanisferioComodin.sql`; la propuesta previa la declara ya desarrollada y activable con credenciales (30 días), dentro de iCONNECT. `[código]` `[datos]`
- **HyperGuest:** sin menciones en Softur.Serenity; la propuesta previa lo plantea como desarrollo nuevo (60 días desde documentación y credenciales). Las integraciones de hoteles viven fuera de este repo, así que el estado actual no se puede confirmar desde el código. `[código]` `[datos]`
- **Travel Compositor:** existe la lectura de reservas (`ReservaTask_CreateFromIntreserva`, alerta en `iControl_EjecucionTareas`). No hay menciones a marketplace ni a Infoterra. `[código]`
- **Web service:** Manual Web Services Bridge y Esquema de llamadas; 20 a 30 días en propuestas previas. `[datos]`
- **Importador:** `ImportReservaAbrevV2` (`IImport_ReservaAbrevV2`) trae `Codigo_de_Agencia` por fila y avisa por mail si el cliente no existe, pero toma los importes del archivo, no del tarifario. Tomar el tarifario se debe adaptar. `[código]`
- **Pax en el ítem:** `ReservaDialog.ts` (línea 3171) sube la cantidad de la máscara si un ítem tiene más pax, nunca la baja; se apaga con `NOTOMOCANTPAXDETRVA`. `[código]`
- **Liquidación:** existen Liquidación, Liquidación Detallada y Preliquidación; `Det_rva` guarda `Comision` y `ComisionPorciento` por ítem. No se encontró un formato con precio por pax y comisión por servicio. `[código]`
- **Caja:** `Caja_List` exporta a Excel y PDF; está en el menú con `ItemClass = "PROF"`. `[código]`
- **Conciliación:** `ConciliacionContable` registra tilde, fecha y usuario; está en el menú con `ItemClass = "SUIT"`. `[código]`
- **Vouchers por tipo de reserva:** `getReportDataReserva` contempla `logoxTIPORVA` y `TIPORVADMC` + informe. No se confirmó un voucher e itinerario completos por tipo. `[código]`

## Archivos, tablas y objetos relevantes
- Entregable: `Trabajo/Entregables/Minuta de reunion - Oportunidades con la migracion a iTraffic (marca Softur).docx`.
- Plantilla: paquete de `Set de Pruebas WS Bridge Prestigio (marca Softur) v2.docx`.
- Softur.Serenity consultado: `Softur.Serene.Web/Modules/E_Ventas/Reserva/ReservaDialog.ts`, `Modules/Z_Reportes/Caja_List`, `Modules/H_Contabilidad/ConciliacionContable`, `Modules/Reports/Templates/Reserva/Liquidacion*`, `Common/Navigation/NavigationItems.cs`, `Modules/N_Varios/Import*`, `Softur.Serene.Model/Modules/E_Ventas/Entities/Det_rvaRow.generated.cs`, y en `Migrations/DefaultDB/ScriptsBD`: `Sp/IImport_ReservaAbrevV2.sql`, `Sp/ReservaTask_CreateFromIntreserva.sql`, `Sp/getReportDataReserva.sql`, `Sp_Configs/PlantillaImport_ReservaAbrevV2.sql`.
- Propuestas previas: `CLIENTES/CARACOL/P - Integracion Hyperguest - Omnibees.docx`, `CLIENTES/INTERCITY/P- Integracion TC INTERCITY.docx`, `CLIENTES/TSA/P - WS iTRAFFIC TSA.docx`, `CLIENTES/EXCURSION AUSTRAL/WS para insercion de reservas - EXCURSION AUSTRAL.docx`.

## Cambios hechos
- Se creó el .docx: resumen, cuatro frentes de oportunidades, puesta en marcha, esquema de tiempos, próximos pasos y cierre comercial. Revisado como PNG.

## Errores y cómo se resolvieron
- `Grep` sobre todo el repo Softur.Serenity vence por tiempo — usar `git grep`. `[datos]`

## Riesgos
- La minuta presenta Omnibees como "se activa"; en la propuesta previa dependía de iCONNECT. Si este cliente no lo tiene, cambia el plazo. `[hipótesis]`
- Conciliación aparece bajo la clase `SUIT` y caja bajo `PROF`; hay que confirmar que entren en la edición que se le venda. `[hipótesis]`

## Pendientes
- [ ] Completar cliente, dueño, fecha y participantes — usuaria.
- [ ] Confirmar el papel de Infoterra y el alcance del marketplace — usuaria.
- [ ] Confirmar quién es Valentina y si los 16 usuarios son licencias o usuarios totales — usuaria.
- [ ] Confirmar si Omnibees requiere iCONNECT para este cliente y el estado de HyperGuest — usuaria / desarrollo.
- [ ] Preparar el documento de requisitos técnicos, el listado de integraciones y el esquema de tiempos: no se encontraron como documentos — usuaria / Softur.

## Cómo validar
Abrir el .docx: 4 páginas, datos a completar resaltados en la portada y secciones 01 a 07.

## Datos que pueden quedar viejos
- Plazos de referencia: Omnibees 30 días, HyperGuest 60, web service 20 a 30, Travel Compositor 45 aprox. — (foto al 2026-11-05)
- Estado de HyperGuest en el repo: sin menciones — (foto al 2026-11-05)
