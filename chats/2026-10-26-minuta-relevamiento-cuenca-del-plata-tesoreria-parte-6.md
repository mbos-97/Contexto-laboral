# Minuta Cuenca del Plata: corrección conceptual de Transportes SaaS

- **Fecha:** 2026-10-26
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria-parte-5.md](2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria-parte-5.md) y [parte-4](2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria-parte-4.md)

## Objetivo
Corregir errores conceptuales señalados por la usuaria: el costeo de "Cuenca del Plata SaaS" es anecdótico porque sucede en otra base de datos; lo que se implementa es la base de Cuenca del Plata.

## Estado final
Terminado. PDF reemplazado y `Minuta de relevamiento - Cuenca del Plata (marca Softur) v3.docx` actualizado (9 páginas).

## Decisiones y por qué
- El operador se llama **Transportes SaaS** (antes "Cuenca del Plata SaaS"). `[decisión]`
- La implementación es de la base de **Cuenca del Plata**. Ahí Transportes SaaS es un operador más: presta el transporte y le factura a Cuenca del Plata. `[decisión]`
- El costeo propio de Transportes SaaS (costos de vehículos por matrícula) se hace en **su propia base de datos** y no forma parte de esta implementación: queda sólo como nota. **Deja sin efecto** el "desarrollo/integración para traer costos por matrícula" y el punto 07.6 de la parte 5, y el detalle de prestadores/vehículos/servicios de costo de SaaS de la parte 4. `[decisión]`
- Bloque en la minuta (página 3): alta del operador → planning con los servicios de transporte asignados a Transportes SaaS (la autorización de pago sale a su nombre) → factura con número de planning → Proveedores controla y Tesorería paga. `[decisión]`
- Sigue vigente la regla de código de la parte 4: la autorización de pago del planning sale al operador del prestador del servicio de costo. `[código]`

## Archivos, tablas y objetos relevantes
- Generador: `minuta.ps1` + `contenido.ps1` + `bloque-saas.ps1` (scratchpad de la sesión).
- Softur.Serenity: no se consultó de nuevo.

## Cambios hechos
- Tabla de Transportes SaaS reducida de 7 a 4 pasos, con nota sobre el costeo en su base; "Qué necesitamos para el primer día" punto 2 = alta del operador; se quitó el punto 07.6.

## Errores y cómo se resolvieron
- Error conceptual: se había tratado el costeo por matrícula de SaaS como parte de la base de Cuenca del Plata — corregido según la usuaria.

## Riesgos
No aplica.

## Pendientes
No aplica.

## Cómo validar
1. PDF página 3: "Transporte: Transportes SaaS como operador", 4 pasos y nota del costeo en su propia base; página 9 sin el punto 6.

## Datos que pueden quedar viejos
No aplica.
