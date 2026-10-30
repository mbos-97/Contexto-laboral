# Tilde Prepago masivo en clientes de iTraffic Cuenca

- **Fecha:** 2026-10-29
- **Proyecto / cliente:** Cuenca del Plata (iTraffic Cuenca)
- **Actualiza a:** [2026-10-28-cartera-clientes-cuenta-corriente-sin-tilde-parte-3.md](2026-10-28-cartera-clientes-cuenta-corriente-sin-tilde-parte-3.md)

## Objetivo
Marcar el tilde Prepago en todos los clientes, salvo CONSUMIDOR FINAL (449), el ID 2949 y los que tienen cuenta corriente.

## Estado final
Terminado y verificado. Se marcaron 4.617 clientes (5 de prueba y 4.612 en lote, sin errores; el lote tardó unos 15 minutos). La verificación final contra el sistema dio 4.744 clientes: 4.619 con Prepago, 124 con cuenta corriente, ninguno con ambos tildes, y el único sin ninguno de los dos es el 2949 (ROSA ANA), excluido a pedido. [datos]

## Decisiones y por qué
- Criterio: Prepago = sí en todo cliente con `Ctacte` = no, salvo los IDs 449 y 2949. [decisión]
- El 2949 en el sistema es "ROSA ANA", no PAX DIRECTO. La usuaria confirmó que se excluye el 2949. El cliente "PAXS DIRECTOS" es el 12250 y ya tenía Prepago. [decisión] [datos]
- Método: la usuaria eligió que lo haga en lote a través del servicio de guardado del sistema (`Services/A_Maestros/Agencia/Update`), enviando sólo `{Prepago: true}`. Antes se probó con 5 clientes, comparando la ficha completa antes y después: el único campo que cambió fue Prepago. [decisión] [datos]

## Archivos, tablas y objetos relevantes
- Softur.Serenity: `Softur.Serene.Web/Modules/A_Maestros/Agencia/AgenciaService.generated.cs`. El `AgenciaSaveHandler` sólo graba el registro y los Textgen, y no tiene lógica extra sobre Prepago. [código]
- `Softur.Serene.Model/Modules/A_Maestros/Entities/AgenciaRow.generated.cs`: la clave es `Cod_agcia`, y los campos `Ctacte` (Concuentacorriente) y `Prepago` son `bool?`. La migración que creó Prepago es `DefaultDB_20260723_233500_AgenciaPrepago`. [código]
- En la pantalla, Maestros → Cliente → Generales → Estadísticas: tilde "Prepago".

## Cambios hechos
- Antes de la carga (foto): 4.744 clientes, 124 con cuenta corriente y 2 con Prepago (449 CONSUMIDOR FINAL y 12250 PAXS DIRECTOS). Había que marcar 4.617: 5 de prueba y 4.612 en lote. [datos]

## Errores y cómo se resolvieron
- `Q.serviceCall` falló desde la consola — se usó `fetch` a `Services/A_Maestros/Agencia/*` con el header `X-CSRF-TOKEN` (cookie `CSRF-TOKEN`).

## Riesgos
- Fue un cambio masivo en producción. Para revertirlo: todo cliente con Prepago, salvo el 449 y el 12250, fue marcado en esta tarea.

## Pendientes
- [ ] Si se dan de alta clientes nuevos, definir si nacen con Prepago — usuaria.

## Cómo validar
Pedir al servicio `List` los campos `Ctacte` y `Prepago`. Tiene que haber 0 clientes sin Ctacte y sin Prepago, sin contar el 2949.

## Datos que pueden quedar viejos
- 4.744 clientes; 124 con cuenta corriente; 4.617 marcados con Prepago en esta tarea — (foto al 2026-10-29)
