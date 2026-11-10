# Reportes de "Cupos Servicios" (ficha operativa): ¿existe uno con cupos disponibles / utilizados / totales?

- **Fecha:** 2026-11-10
- **Proyecto / cliente:** Softur / Serenity — ficha operativa, pantalla "Nuevo Cupos Servicios"
- **Actualiza a:** No aplica

## Objetivo
Saber si en el combo "Tipo" de Cupos Servicios ya existe un reporte con fecha, reserva, servicio, cupos disponibles, utilizados y totales.

## Estado final
Terminado. Respuesta: **sí hay dos parecidos, ninguno igual**:
- **Tipo 01** (cupos de servicios, tabla `Bloserv`): columnas `nombre_serv`, `fecha_cupo`, `categoria`, `hora_blo`, `Cupo` (total = `con_hab`), `Rva` (cantidad usada = suma de `det_rvah.cantiphab` de las reservas de ese servicio, fecha y categoría, excluyendo estados operativos de `parame` STSC), `Dispo` (= Cupo − Rva). Es por servicio y fecha, **no muestra número de reserva**. `[código]`
- **Tipo 60 "CUPOS SALIDAS PAQUETES"** (tabla `Fec_paq`): `paquete`, `fecha` de salida, `clave` (cod_cupo), `lugares` (total), `vendidos` (`fsp_getCupoPaquetebysalida`), `disponibles`, `estado`. Es por paquete/salida, no por servicio ni reserva. `[código]`
- El tipo 01 **no figura en el combo por defecto**: el combo lee `parame` código `CUTI` y no hay alta para el retorno `01`. Si el Tipo viene vacío el SP usa `60`. Para verlo bastaría agregar la fila `CUTI` / `01` en `parame` (configuración, no desarrollo). `[código]`
- Ningún tipo muestra el detalle por reserva (número de reserva + cupos que consume) junto a total/usado/disponible: eso sería un tipo nuevo o una ampliación del 01. `[código]`

## Decisiones y por qué
No aplica (consulta).

## Archivos, tablas y objetos relevantes
- Repo Softur.Serenity: `Softur.Serene/Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/IFO_Get_CuposServ.sql` (bloques `@tipocupoficha` 01 ≈ línea 339, 60 ≈ línea 1576; altas `CUTI` al final). Variante `IFO_Get_CuposServ_mendoza.sql` (config `LSPESPACIALCUPOSERV`), con el mismo esquema del tipo 01.
- `Sp_Configs/ParameDefaultInsert_Aprobaciones.sql`: altas `CUTI` 07, 08, 60, 61, 70, 71, 72, 76.
- Tablas: `Bloserv`, `servicio`, `det_rva`, `det_rvah`, `Fec_paq`, `Paquete`, `parame` (CUTI, STSC), `config` (TIPOCUPOFICHA, LSPESPACIALCUPOSERV).

## Cambios hechos
Ninguno en el sistema.

## Errores y cómo se resolvieron
- Grep sobre todo el repo excedía el tiempo — se usó `git grep` excluyendo migraciones.

## Riesgos
Agregar el tipo 01 al combo en una base de cliente lo deja visible para todos los usuarios de esa base. `[hipótesis]`

## Pendientes
- [ ] Definir si se pide a desarrollo un tipo nuevo con número de reserva — usuaria.

## Cómo validar
En una base de prueba, insertar `parame` (CUTI, 'CUPOS SERVICIOS', '01') y elegirlo en Nuevo Cupos Servicios con un rango de fechas con bloqueos cargados.

## Datos que pueden quedar viejos
- Tipos CUTI dados de alta en scripts: 06, 07, 08, 60, 61, 70, 71, 72, 76, 77, 80–87 (foto al 2026-11-10).
