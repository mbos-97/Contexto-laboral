# Propuesta comercial Importador Despegar + Interfaz Get Your Guide para Marpatag (marca Softur)

- **Fecha:** 2026-11-16
- **Proyecto / cliente:** Softur — iTRAFFIC, cliente Marpatag
- **Actualiza a:** ninguna (adapta una propuesta de mayo 2025 hecha para Pingüinos Expediciones)

## Objetivo
Pasar a marca Softur y a Marpatag la propuesta "Importador de reservas Despegar + Interfaz lectura de reservas GyG" de Pingüinos Expediciones, con los mismos precios y prestaciones y mejor redacción.

## Estado final
Terminado, 4 páginas. `Trabajo/Entregables/Propuesta comercial - Importador Despegar e Interfaz Get Your Guide - Marpatag (marca Softur).docx` y `.pdf`.

## Decisiones y por qué
- Precios y prestaciones iguales al original (pedido de la usuaria): `[decisión]`
  - Importador de reservas Despegar: setup USD 600, soporte USD 50/mes.
  - Interfaz Get Your Guide: setup USD 950, soporte USD 50/mes. Total USD 1.550 + USD 100/mes, sin IVA.
  - Plazo 45 a 60 días aprox. desde el ingreso del proyecto en agenda. Pago 50% anticipo / 30% a 30 días / 20% al pase a producción (montos calculados: USD 775 / 465 / 310).
  - Se mantienen: homologación por única vez (CodHomologos), mapeos a cargo del cliente, Softur no negocia con los proveedores, criterios de aceptación, lugar de trabajo y confidencialidad.
- Estructura: portada con datos y tabla de integraciones; 01 Despegar y 02 Get Your Guide con "Cómo funciona" en pasos numerados y capturas; 03 Costos, plazos y forma de pago; 04 Condiciones generales. `[decisión]`
- No se puso vigencia (el original vencía al mes; en PaxDirect Marpatag se había quitado). `[hipótesis]`
- Se reutilizaron las 4 capturas del original (Importar Info, CodHomologos, portal GYG, listado de reservas GYG); CodHomologos muestra hoteles de Ushuaia de la base de Pingüinos. `[datos]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity (sólo lectura): el `git pull` falló (sin conexión a tfs.softur.com.ar:8080); se buscó en la copia local: `[código]`
  - Despegar: migración `Softur.Serene.Model/Migrations/DefaultDB/DefaultDB_20210630_120000_ImpRvaDespegar.cs`.
  - Get Your Guide: `ScriptsBD/Sp/GetYourGuide_Inventary_AddDelMod.sql`, `GetYourGuide_Inventary_Update.sql`, `GetYourGuide_SearchAvaibilities.sql`; tablas `ScriptsBD/Tables/GetYourGuide_Bookings.sql`, `GetYourGuide_Inventary.sql`.
- Plantilla: paquete de `Propuesta de requerimientos - Marpatag (marca Softur) v2.docx`.
- Generador: script PowerShell en el scratchpad de la sesión (no persistente).

## Cambios hechos
- Se creó el .docx y el .pdf en Entregables. Nada modificado en Softur.Serenity.

## Errores y cómo se resolvieron
- Abrir un PDF con Word por COM queda colgado (diálogo de conversión invisible): se mató el WINWORD `/Automation` y se extrajeron las imágenes del PDF leyendo los XObject (`DCTDecode` = JPEG directo; `FlateDecode` RGB = descomprimir con `DeflateStream` salteando 2 bytes y armar un Bitmap).
- PowerShell no distingue mayúsculas en variables: `$s` pisó a `$S` dentro de una función. Usar nombres distintos.

## Riesgos
- Falta de vigencia y las capturas con datos de Pingüinos pueden no ser lo deseado. `[hipótesis]`

## Pendientes
- [ ] Revisar y enviar la propuesta a Marpatag — usuaria.

## Cómo validar
PDF de 4 páginas: portada; p. 2 Despegar con 2 capturas y link al formato modelo; p. 3 Get Your Guide con 2 capturas; p. 4 costos (USD 1.550 + USD 100/mes) y condiciones.

## Datos que pueden quedar viejos
- Precios del original de mayo 2025 — (foto al 2026-11-16)
