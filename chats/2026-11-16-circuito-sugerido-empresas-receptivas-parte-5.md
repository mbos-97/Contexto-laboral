# Circuito sugerido para empresas receptivas — corrección de autorización de pago, maestros en el esquema y recuadros

- **Fecha:** 2026-11-16
- **Proyecto / cliente:** Softur — material genérico de implementación iTRAFFIC (receptivos)
- **Actualiza a:** [2026-11-16-circuito-sugerido-empresas-receptivas-parte-4.md](2026-11-16-circuito-sugerido-empresas-receptivas-parte-4.md)

## Objetivo
Corregir el esquema y el texto según la usuaria: por defecto la autorización de pago la cargan los usuarios imputando al planning; el esquema no mostraba "Inicio: carga de maestros"; pidió texto justificado y permitió recuadros de color.

## Estado final
Terminado. `Trabajo/Entregables/Circuito sugerido para empresas receptivas (marca Softur).docx` (+ `.pdf`) reemplazados, siguen en 3 páginas.

## Cambios hechos
- Esquema: "Inicio" → "Inicio: carga de maestros"; "Planning en estado 'Autorizar pago'" → "Generación de planning"; "Autorización de pago automática" → "Autorización de pago imputando al planning"; "Autorización de pago manual contra la reserva" → "Autorización de pago imputando a la reserva" (para que no quede el contraste manual/automática).
- Sección 03: se quitó que el estado "Autorizar pago" genera la autorización; ahora dice que, con el planning armado, el usuario carga la autorización (paso 04).
- Sección 04: recuadro naranja "Regla clave" (ningún pago sin autorización; el usuario carga cada autorización y la imputa al planning o a la reserva). "Con planning": cargar la autorización en Proveedores › Autorización Pagos imputándola a los ítems del planning.
- Sección 04: se quitó la viñeta opcional del botón "Autorizar" (doble control); no va en el documento genérico.
- Sección 08: las viñetas pasan a un recuadro Arena "Control diario".
- Todo el texto justificado (párrafos, viñetas y recuadros).

## Decisiones y por qué
- En los documentos de proceso **sí** se permiten recuadros de color y el texto va justificado (pedido de la usuaria; antes había rechazado recuadros en la versión larga). `[decisión]`
- Autorización de pago con planning: por defecto la carga el usuario imputando al planning. Hay procesos donde se automatiza (estado `A` del planning genera las AUT, visto en código), pero **no se menciona la automatización** en el documento: se explica como carga e imputación del usuario, sin resaltar que "no es automática". `[decisión]` (pedido de la usuaria)

## Archivos, tablas y objetos relevantes
- Generador (scratchpad, no persiste): `gen4.ps1` + `contenido4.ps1` + `Diagrama3.cs` (se compila con Windows PowerShell 5.1, no con pwsh 7: falta `System.Drawing.Primitives`).
- Softur.Serenity: no se consultó código nuevo.

## Errores y cómo se resolvieron
- `Add-Type` del diagrama falla en pwsh 7 — tipos reenviados a `System.Drawing.Primitives` — correr `diagrama3.ps1` y `run4.ps1` con `powershell.exe`.

## Pendientes
- [ ] Probar "?nro de planning" al imputar factura de proveedor (y en la autorización) — implementación.

## Cómo validar
1. PDF de 3 páginas; esquema con "Inicio: carga de maestros" y "Generación de planning"; recuadros en 04 y 08.

## Datos que pueden quedar viejos
No aplica.
