# Correo de migración Traffic → iTraffic: salidas grupales y ficha operativa

- **Fecha:** 2026-11-06
- **Proyecto / cliente:** Cliente con Traffic (Fox); nombre pendiente
- **Actualiza a:** [2026-11-05-minuta-comercial-migracion-traffic-a-itraffic-parte-2.md](2026-11-05-minuta-comercial-migracion-traffic-a-itraffic-parte-2.md)

## Objetivo
Sumar al correo al dueño el módulo de salidas grupales con autorregistro de pasajeros para la gestión estudiantil, y la implementación completa de la ficha operativa.

## Estado final
Terminado: correo actualizado en el chat. Falta confirmar con la usuaria dónde vive el autorregistro.

## Decisiones y por qué
- La ficha operativa pasa de "sesión con Valentina" a punto propio de implementación: registro de servicios, pedidos a operadores, asignación de guías y órdenes de servicio. `[decisión]`
- Grupos y estudiantil se presentan como un frente propio. `[decisión]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity (`git pull` hecho): módulo `M_Estudiantil` (Grupos/Contrato, Planes/Cuotacol, Recargos, TipoPaxGrupos, chequeras y cuotas), con `ItemClass = "STUD"` en `NavigationItems.cs`. `[código]`
- Autorregistro de pasajeros: sin menciones en Softur.Serenity (se buscó autoregistro, inscripción, salidas grupales). Puede ser una app aparte o un desarrollo. `[hipótesis]`
- Ficha operativa: órdenes de servicio (`FICHAOPE`), pedidos a proveedores (`PEDIDOPER`), guía por ítem (un solo guía por ítem). Ver [2026-10-13-guia-rapida-ficha-operativa-con-marca-parte-2.md](2026-10-13-guia-rapida-ficha-operativa-con-marca-parte-2.md) y [2026-10-27-nuevo-proceso-por-sector-cuenca-del-plata-parte-2.md](2026-10-27-nuevo-proceso-por-sector-cuenca-del-plata-parte-2.md). `[código]`

## Cambios hechos
- Sólo redacción del correo.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Si el autorregistro no existe como producto, el correo lo vende como disponible. `[hipótesis]`
- El módulo estudiantil es de la clase `STUD`: confirmar que entre en lo que se le venda. `[hipótesis]`
- Varios guías por ítem requiere desarrollo. `[código]`

## Pendientes
- [ ] Confirmar si el autorregistro de pasajeros existe y dónde — usuaria.

## Cómo validar
Revisar el correo: frente de grupos y estudiantil, y ficha operativa con los cuatro puntos.

## Datos que pueden quedar viejos
No aplica.
