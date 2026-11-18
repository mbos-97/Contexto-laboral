# Manual iConnect Marpatag — imagen del servicio

- **Fecha:** 2026-11-13
- **Proyecto / cliente:** Marpatag — iConnect
- **Actualiza a:** [2026-11-13-manual-uso-iconnect-marpatag-parte-3.md](2026-11-13-manual-uso-iconnect-marpatag-parte-3.md)

## Objetivo
La usuaria indicó que la imagen sale de la imagen cargada en el servicio (código 1230). Había que ver dónde la usa iConnect.

## Estado final
Hecho. En la página de detalle (`/servicera`), iConnect pone la primera imagen de la solapa **Imagenes** del servicio (`upload/IMAGENSERVICIOs/00001/00001230_….png`) como `og:image`. Con ella van `og:title` = NOMBRE SERVICIO WEB y `og:description` = nombre + Observaciones. Es la **vista previa del enlace** al compartirlo; no hay ningún `<img>` visible en el detalle, el listado ni el carrito. `[datos]`
Manual regenerado (23 páginas): en la sección 06 se sumó "Imagen del servicio" con la captura de la solapa Imagenes. El pendiente 8 quedó como "confirmar si debería verse también dentro del detalle".

## Cambios hechos
Ninguno en el sistema.

## Pendientes
- [ ] Confirmar con la usuaria o con desarrollo si la imagen debería mostrarse en pantalla (hoy sólo es la vista previa del enlace).
