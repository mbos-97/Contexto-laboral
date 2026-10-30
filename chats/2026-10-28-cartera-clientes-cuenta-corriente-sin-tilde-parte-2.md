# Cruce cartera CC vs tilde Concuentacorriente: duplicados excluidos

- **Fecha:** 2026-10-28
- **Proyecto / cliente:** Uso interno (cartera de clientes con cuenta corriente autorizada)
- **Actualiza a:** [2026-10-28-cartera-clientes-cuenta-corriente-sin-tilde.md](2026-10-28-cartera-clientes-cuenta-corriente-sin-tilde.md)

## Objetivo
Resolver el pendiente de los registros duplicados de Almundo y Pezzati.

## Estado final
Terminado.

## Decisiones y por qué
- Los registros adicionales ALMUNDO PRE COMPRA (3464) y EDUARDO PEZZATI (12060) no llevan el tilde y se sacan del listado. Para esos clientes alcanza con el registro principal, que ya lo tiene. [decisión]

## Archivos, tablas y objetos relevantes
- `Entregables/Clientes cartera sin cuenta corriente 2026-10-28.xlsx`: la hoja `Resumen` quedó con 24 filas (15 FALTA TILDE y 9 OK).
- No se consultó Softur.Serenity.

## Cambios hechos
- Se borraron las filas "REVISAR" de `Resumen` y se actualizó la nota.
- En la hoja `Clientes` se limpiaron las marcas y el color de esos dos registros.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
No aplica.

## Pendientes
- [ ] Poner el tilde a los 15 registros "FALTA TILDE" — usuaria/administración.

## Cómo validar
En `Resumen` no tiene que quedar ninguna fila "REVISAR".

## Datos que pueden quedar viejos
- Registros sin tilde: 15; ya con tilde: 9 — (foto al 2026-10-28)
