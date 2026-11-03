# Set de pruebas WS Bridge Avioa con marca Softur

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Avioa Operador Mayorista — WebService Bridge de iTraffic
- **Actualiza a:** No aplica. Sigue el formato de [2026-11-03-set-pruebas-ws-bridge-prestigio-marca-softur-parte-3.md](2026-11-03-set-pruebas-ws-bridge-prestigio-marca-softur-parte-3.md)

## Objetivo
Pasar el set de pruebas a la marca Softur, como el de Prestigio, y aclarar que el web service apunta al entorno de test y que ese entorno se actualizó por última vez el 15/10.

## Estado final
Terminado (10 páginas), con datos para revisar antes de compartirlo.

## Decisiones y por qué
- Se tomó como documento el último set descargado (`Set_de_Pruebas_WS_Bridge_Avioa_Actualizado.docx`): el pedido no traía adjunto. [hipótesis]
- Portada con aviso "Entorno de test": apunta al entorno de test, endpoint del documento y última actualización 15/10/2026. El año se infirió de la fecha actual. [decisión]
- No se agregó "credenciales iguales a producción" ni una URL de iTraffic test: eran datos de Prestigio y no se indicaron para Avioa. [decisión]
- Claves y pasajeros quedan sin enmascarar, como en Prestigio. [hipótesis]
- El texto, los RQ y los RS quedan sin cambios; sólo se separó en dos viñetas el párrafo de `dateFrom`/`dateTo` y `dateType`. [decisión]

## Archivos, tablas y objetos relevantes
- Original: `Downloads/Set_de_Pruebas_WS_Bridge_Avioa_Actualizado.docx` (sin tocar).
- Nuevo: `Trabajo/Entregables/Set de Pruebas WS Bridge Avioa (marca Softur).docx`.
- Molde: `Trabajo/Entregables/Set de Pruebas WS Bridge Prestigio (marca Softur) v2.docx`.
- Softur.Serenity: no se consultó; no se agregaron datos de producto.

## Cambios hechos
- Se reutilizó el paquete del set de Prestigio v2 (estilos, fuentes, logo, banda de encabezado, pie) y se reemplazaron portada y cuerpo.
- Control automático: todos los párrafos del original siguen, salvo título y subtítulo, que pasan a la portada con el formato de marca.

## Errores y cómo se resolvieron
- "Estado" se partía en dos líneas en la matriz — columna angosta — se ensanchó.
- Un heredoc largo en Git Bash se cortó al crear el script — se escribieron los archivos con la herramienta de escritura.
- `perl` no está en el PATH de PowerShell — correrlo desde Git Bash.

## Riesgos
- Quedan a la vista credenciales, IP del servidor y datos de pasajeros reales. [datos]
- La matriz cita "Rochester Bariloche", que no aparece en ningún RS del documento. [datos]
- La matriz muestra "$772.060,99", pero la reserva 34616 está en `Currency="COP"`. [datos]
- La reserva 30137 figura como "reserva estándar", pero está cancelada (`Status="CxL"` / `"CX"`) y sin servicios. [datos]

## Pendientes
- [ ] Confirmar que era este el documento y el año de la actualización — usuaria.
- [ ] Revisar los tres puntos de datos de la matriz antes de compartir — usuaria.

## Cómo validar
Abrir el .docx en Word: 10 páginas, aviso de test en la portada y banda negra de borde a borde en las páginas interiores.

## Datos que pueden quedar viejos
- Entorno de test actualizado al 15/10/2026 — (foto al 2026-11-03)
- Pruebas validadas el 03/11/2026 — (foto al 2026-11-03)
