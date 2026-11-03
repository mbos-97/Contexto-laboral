# Set de pruebas WS Bridge Prestigio con marca Softur

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Prestigio / Patagonia Sur — WebService Bridge de iTraffic
- **Actualiza a:** No aplica

## Objetivo
Pasar el set de pruebas a la marca Softur, aclarar en la portada que el web service apunta a la base de test y quitar la nota sobre Smart/Traffic y el petrel.

## Estado final
Terminado (20 páginas), con dudas para revisar antes de compartirlo.

## Decisiones y por qué
- Portada con aviso "Entorno de test": apunta a la base de test, URL de test, credenciales iguales a producción, base actualizada al 15/10/2026. El año lo inferí de la fecha actual. [decisión]
- De la nota de compatibilidad se quita Smart/Traffic, la contraseña y la referencia al petrel; queda sólo que las claves se validan en mayúsculas, porque el texto de la sección anuncia particularidades de autenticación. [decisión]
- "Base de Datos Asignada" pasa de `iTraffic_Prestigio` a "Test" para no contradecir la portada; no se escribió un nombre de base porque no está confirmado. [hipótesis]
- El resto del texto, los RQ y los RS quedan sin cambios: son evidencia de las pruebas. [decisión]
- "patagónico" sigue en la descripción de una excursión y `ListSmart` en un esquema de la respuesta: son datos del servicio, no parte de la nota. [datos]

## Archivos, tablas y objetos relevantes
- Original: `Downloads/Set_de_Pruebas_WS_Bridge_Prestigio.docx` (sin tocar).
- Nuevo: `Trabajo/Entregables/Set de Pruebas WS Bridge Prestigio (marca Softur).docx`.
- Softur.Serenity: no se consultó; no se agregaron datos de producto.

## Cambios hechos
- Se tomó como base el paquete de la propuesta de TODO WAY v2 (estilos, fuentes embebidas, logo, encabezado y pie) y se reemplazó el cuerpo.
- Margen superior de 1480 dxa para que el contenido no toque el logo del encabezado.
- Control automático: todos los párrafos del original siguen tal cual, salvo subtítulo, base de datos y nota.

## Errores y cómo se resolvieron
- Texto pegado al logo cuando la página no arranca con un título — margen superior chico — subir el margen a 1480 dxa.

## Riesgos
- Quedan a la vista claves válidas también en producción, IP del servidor y rutas internas. [datos]
- Las respuestas de `getBooking` traen datos de pasajeros reales. [datos]
- El error citado en el diagnóstico muestra una ruta con el nombre de otra instalación (`WSBridge_Euro_Time`). [datos]

## Pendientes
- [ ] Decidir si se enmascaran claves y pasajeros antes de compartir — usuaria.
- [ ] Confirmar el nombre de la base de test y si el endpoint `.WS.TEST` es el vigente — usuaria.

## Cómo validar
Abrir el .docx en Word: 20 páginas, aviso de test en la portada y sin la frase del petrel en la sección 2.

## Datos que pueden quedar viejos
- Base de test actualizada al 15/10/2026 — (foto al 2026-11-03)
- Pruebas validadas el 03/11/2026 — (foto al 2026-11-03)
