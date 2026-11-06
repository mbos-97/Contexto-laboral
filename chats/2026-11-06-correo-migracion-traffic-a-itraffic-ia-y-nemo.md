# Correo de migración Traffic → iTraffic: tono formal, IA y lectura de ventas de Nemo

- **Fecha:** 2026-11-06
- **Proyecto / cliente:** Cliente con Traffic (Fox); nombre pendiente
- **Actualiza a:** [2026-11-06-correo-migracion-traffic-a-itraffic-grupos-y-ficha.md](2026-11-06-correo-migracion-traffic-a-itraffic-grupos-y-ficha.md)

## Objetivo
Pasar la apertura del correo a un tono más formal: revisión hecha con Jonathan, migración como necesidad técnica impostergable y foco en que iTraffic es superadora y optimiza procesos manuales. Sumar los desarrollos con IA (iAGENT y asistente) y la lectura de ventas desde Nemo.

## Estado final
Terminado: correo completo actualizado en el chat.

## Decisiones y por qué
- Se elimina "Te lo digo directo"; se usa "impostergable" en lugar de "imperiosa". `[decisión]`
- El cierre de la apertura pone el foco en la herramienta y en el tiempo que libera, no en el acompañamiento al equipo. `[decisión]`
- Nuevo frente: inteligencia artificial (iAGENT B2C sobre todo el inventario de iTraffic, con versión B2B próximamente; asistente de IA para usuarios). `[decisión]`
- Nemo va en "menos carga manual": lectura de ventas para evitar la carga y los errores humanos. `[decisión]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity (`git pull` hecho): asistente de IA en `Softur.Serene.Web/Modules/Common/AI/AIAssistantController.cs` (chat con contexto de la pantalla, modos ayuda y finanzas, acciones) y filtros por lenguaje natural en el listado de reservas (`Modules/Z_Reportes/Reserva_List/AI/Reserva_ListSemanticDictionary.cs`). `[código]`
- iAGENT y Nemo: sin menciones en Softur.Serenity; se toman de lo que dijo la usuaria. `[hipótesis]`

## Cambios hechos
- Sólo redacción.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Si la lectura de Nemo requiere desarrollo, el correo la presenta como disponible. `[hipótesis]`

## Pendientes
- [ ] Confirmar el estado de la lectura de ventas de Nemo y de iAGENT — usuaria.

## Cómo validar
Revisar el correo: apertura formal y frente de IA.

## Datos que pueden quedar viejos
- iAGENT: B2C disponible y B2B "próximamente" — (foto al 2026-11-06)
