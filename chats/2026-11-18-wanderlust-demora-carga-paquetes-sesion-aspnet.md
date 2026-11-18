# Wanderlust: demora al cargar paquetes en la reserva (análisis de devolución de i2Server)

- **Fecha:** 2026-11-18
- **Proyecto / cliente:** Wanderlust (servidor gestionado por i2Server, migración de prueba)
- **Actualiza a:** No aplica

## Objetivo
Interpretar la devolución técnica de i2Server (agregar paquete WE TRF IN KNAP al file MBE 541 tarda ~19 s, a veces 35 s, con "la página no responde") y definir qué ajustar técnicamente.

## Estado final
Terminado (análisis). Ajustes propuestos para desarrollo; nada implementado.

## Decisiones y por qué
- La hipótesis de i2Server es consistente con el código: la sesión ASP.NET está activa en modo completo (InProc, `<sessionState timeout="30" />`) y ningún controller declara `SessionState` ReadOnly/Disabled → pedidos simultáneos del mismo usuario se serializan y los que esperan reintentan cada 500 ms. [código]
- Los endpoints de servicios no usan `Session`: sólo se usa en `AccountPage.cs` (forceLogout) y `LoginLimitAttribute.cs` (aplicado únicamente en `DashboardPage`). Poner la sesión en ReadOnly para `/Services/*` es de bajo riesgo. [código]
- El cartel "la página no responde" lo causan las llamadas sincrónicas (`async: false`) del front, que bloquean el navegador; hay 268 en Modules y varias en el flujo de alta de ítems de la reserva (ReCostearItem por ítem, AgenciaService.Retrieve dentro de un forEach de servicios automáticos). [código]
- La causa raíz no es servidor ni SQL (coincide con la medición del cliente: SQL ~4–5 s de 19 s). [datos de i2Server] / [hipótesis hasta re-medir]

## Archivos, tablas y objetos relevantes
- `Softur.Serene/Softur.Serene.Web/Web.config` línea ~137: `<sessionState timeout="30" />`.
- `Softur.Serene.Web/Global.asax.cs` (Application_BeginRequest sin manejo de sesión).
- `Modules/Common/Helpers/LongRunningActionController.cs` (base de ReservaController, hereda ServiceEndpoint).
- `Modules/E_Ventas/Reserva/ReservaEndpoint.generated.cs` (ReCostearItem, ProcesarServiciosAuto), `ReservaService.cs`.
- `Modules/E_Ventas/Reserva/ReservaDialog.ts` (~línea 1253 ReCostearItem async:false; ~3194 ProcesarServiciosAuto; ~3253 AgenciaService.Retrieve async:false dentro de forEach).
- `Modules/A_Maestros/Servicio/ServicioEndpoint.cs` (RetrieveServ) y `Provedor/ProvedorEndpoint.cs` (RetrieveHotel), invocados desde `Modules/E_Ventas/Det_rva/TarifaServLazyEditor.ts` / `TarifaHotelLazyEditor.ts`.
- `Modules/Membership/Account/AccountPage.cs`, `LoginLimit/LoginLimitAttribute.cs`, `Modules/Dashboard/DashboardPage.cs`.
- SP `iTarifaServ_ListSmart` (~0,8 s, consulta más larga reportada).

## Cambios hechos
No aplica (sólo análisis; repo Softur.Serenity en sólo lectura).

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Si algún endpoint futuro escribe en `Session`, con ReadOnly el cambio no persiste (no da error). Hoy ninguno lo hace.
- Quitar `async: false` cambia el orden de ejecución en el diálogo de reserva: requiere refactor con promesas y pruebas de regresión.

## Pendientes
- [ ] Desarrollo: sesión ReadOnly para `/Services/*` (controller factory propio o atributo en una base común) — desarrollo.
- [ ] Desarrollo: eliminar `async: false` y llamadas repetidas en el alta de paquetes; evaluar ReCostear en lote — desarrollo.
- [ ] Re-medir con i2Server el mismo caso (MBE 541 + WE TRF IN KNAP) tras el ajuste.

## Cómo validar
Repetir el caso de prueba en el servidor de pruebas; en los logs de IIS (`time-taken`) deben desaparecer los tiempos en múltiplos de ~500 ms y el tiempo total debería acercarse al tiempo real de SQL.

## Datos que pueden quedar viejos
- Tiempo del caso — ~19 s (picos 35 s), ~20 pedidos IIS — (foto al 2026-11-18)
- Llamadas `async: false` en Modules — 268 — (foto al 2026-11-18)
