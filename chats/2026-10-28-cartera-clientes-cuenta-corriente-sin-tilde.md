# Cruce cartera de clientes con cuenta corriente vs tilde Concuentacorriente

- **Fecha:** 2026-10-28
- **Proyecto / cliente:** Uso interno (cartera de clientes con cuenta corriente autorizada)
- **Actualiza a:** No aplica

## Objetivo
Del listado completo de clientes y agencias exportado del sistema (~4.700 registros), identificar los que figuran en la planilla "CARTERA CLIENTES" (clientes con cuenta corriente autorizada) y que todavía no tienen el tilde `Concuentacorriente`.

## Estado final
Terminado. Excel de resultado generado en `Entregables`.

## Decisiones y por qué
- El cruce se hizo por nombre (columnas `Nombre` y `Nombre Completo`), sin tener en cuenta mayúsculas ni tildes, porque la cartera sólo trae nombres de fantasía, sin ID ni CUIT. [datos]
- "DANIELA" (primera fila de la cartera) se tomó como encabezado o responsable, no como cliente. [hipótesis]
- "SAT BR" se tomó como el registro SAT BRASIL. "LATITUR - TUR.COM" se tomó como dos registros: LATITUR SAS y TUR.COM SPA. [hipótesis]
- En SOL IGUAZU se tomó la agencia, no los registros de cabañas que también tienen ese nombre. [hipótesis]
- ALMUNDO y PEZZATI tienen un registro con tilde y otro adicional sin tilde (ALMUNDO PRE COMPRA, EDUARDO PEZZATI): esos registros adicionales se marcaron "REVISAR". [datos]

## Archivos, tablas y objetos relevantes
- Entrada: export `ClientesyagenciasList_<fecha>.xlsx` (hoja Page1; columnas ID, Código, Nombre, Nombre Completo, …, Condicion, Concuentacorriente con VERDADERO/FALSO) y `CARTERA CLIENTES.xlsx` (Hoja1, columna B).
- Salida: `Entregables/Clientes cartera sin cuenta corriente 2026-10-28.xlsx`, con la hoja `Resumen` (26 filas por estado) y la hoja `Clientes` (el listado completo con las columnas `Cartera CC` y `Estado cartera`, filas coloreadas y autofiltro).
- No se consultó Softur.Serenity, porque fue un cruce de planillas.

## Cambios hechos
Se generó el Excel de resultado. No se modificó nada en el sistema.

## Errores y cómo se resolvieron
- Un OrderedDictionary de PowerShell con claves `int` toma el indexador como posición y devuelve null. Se usó un hashtable con claves string.

## Riesgos
- Al cruzar por nombre puede pasar que un cliente esté cargado con otra razón social y no aparezca. Hay que validar los casos marcados como hipótesis.

## Pendientes
- [ ] Poner el tilde a los 15 registros "FALTA TILDE" — usuaria/administración.
- [ ] Confirmar qué se hace con ALMUNDO PRE COMPRA y EDUARDO PEZZATI — usuaria.

## Cómo validar
Abrir la hoja `Clientes`, filtrar `Estado cartera` = "FALTA TILDE" y controlar que `Concuentacorriente` = FALSO.

## Datos que pueden quedar viejos
- Clientes en cartera — 24 (sin contar DANIELA) — (foto al 2026-10-28)
- Registros sin tilde: 15; a revisar: 2; ya con tilde: 9 — (foto al 2026-10-28)
- Clientes con tilde en el sistema — 109 de 4.744 — (foto al 2026-10-28)
