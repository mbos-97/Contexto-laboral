# Minuta Cuenca del Plata: costo del transporte SaaS por matrícula

- **Fecha:** 2026-10-26
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria-parte-4.md](2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria-parte-4.md)

## Objetivo
Sumar que el transporte de Cuenca del Plata SaaS se costea por vehículo, por matrícula, con los costos de la base de datos de SaaS.

## Estado final
Terminado. PDF reemplazado y `Minuta de relevamiento - Cuenca del Plata (marca Softur) v3.docx` actualizado (9 páginas).

## Decisiones y por qué
- El costo del transporte SaaS se toma por matrícula de vehículo desde la base de datos de Cuenca del Plata SaaS. `[decisión]`
- iTraffic ya tiene el campo `Matricula` en el vehículo (también `Espropio` y `Cod_prov` = prestador). `[código]`
- Ningún SP del directorio de scripts usa `Matricula`: hoy el costo del planning sale de la tarifa del servicio de costo (filtrada por prestador y fecha) y no hay lectura de otra base. Traer los costos por matrícula desde SaaS es un desarrollo/integración a definir. `[código]` (búsqueda en `ScriptsBD/Sp`; la búsqueda de "saas" en todo el repo no terminó por tiempo)
- La tabla de pasos de Cuenca del Plata SaaS pasa a 7 pasos (nuevo paso 4 "Costo por matrícula"); el punto 07.6 queda como "Costo de Cuenca del Plata SaaS por matrícula: importación o integración, frecuencia y fecha de inicio; requiere desarrollo". `[decisión]`

## Archivos, tablas y objetos relevantes
- `Softur.Serene.Model/Modules/J_Receptivo/Entities/VehiculoRow.generated.cs` — campos `Matricula`, `Espropio`, `Cod_prov`, `Vigdesde`/`Vighasta`.
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/` — sin referencias a `Matricula`.

## Cambios hechos
- Página 3 de la minuta: paso 4 nuevo, renumerados 5–7; "Qué necesitamos para el primer día" pide vehículos con matrícula; punto 07.6 reescrito.

## Errores y cómo se resolvieron
- La búsqueda de "saas" en todo el repo superó el tiempo — se acotó a la carpeta de SPs.

## Riesgos
- Mientras no exista la integración, el costo del transporte SaaS tendría que cargarse como tarifa de servicio de costo en iTraffic. `[hipótesis]`

## Pendientes
- [ ] Definir con desarrollo cómo se traen los costos por matrícula desde la base de SaaS (importación o integración) y estimarlo — usuaria / desarrollo.

## Cómo validar
1. PDF página 3: tabla de Cuenca del Plata SaaS con 7 pasos, el 4 es "Costo por matrícula".

## Datos que pueden quedar viejos
No aplica.
