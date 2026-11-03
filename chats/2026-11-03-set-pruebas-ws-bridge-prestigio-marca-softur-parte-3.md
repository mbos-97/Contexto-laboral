# Set de pruebas WS Bridge Prestigio: encabezado de borde a borde

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Prestigio / Patagonia Sur — WebService Bridge de iTraffic
- **Actualiza a:** [2026-11-03-set-pruebas-ws-bridge-prestigio-marca-softur-parte-2.md](2026-11-03-set-pruebas-ws-bridge-prestigio-marca-softur-parte-2.md)

## Objetivo
Reemplazar el recuadro negro chico del logo en el encabezado por una banda que ocupe todo el ancho de la página.

## Estado final
Terminado (20 páginas). Se generó la versión v2.

## Decisiones y por qué
- El encabezado de las páginas interiores es una banda Tinta de borde a borde, con el logo a la derecha, alineado con el margen del texto: a la usuaria el recuadro chico le parecía feo. [decisión]
- La portada no cambia su diseño: no usa ese encabezado. [decisión]
- Se guarda como archivo nuevo porque el anterior estaba abierto en Word. [datos]

## Archivos, tablas y objetos relevantes
- Vigente: `Trabajo/Entregables/Set de Pruebas WS Bridge Prestigio (marca Softur) v2.docx`.
- Softur.Serenity: no se consultó.

## Cambios hechos
- `word/header1.xml`: tabla de una celda de 11906 dxa, con sangría de -1080 dxa y fondo `191917`.
- Márgenes de la sección: encabezado en 0 y superior en 1300 dxa.
- El texto no cambió: se partió de la versión guardada por la usuaria en Word.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
La propuesta de TODO WAY v2 sigue con el recuadro chico. [datos]

## Pendientes
- [ ] Decidir si la propuesta de TODO WAY lleva la misma banda — usuaria.

## Cómo validar
Abrir el .docx en Word: la banda negra llega a los dos bordes y al borde superior en todas las páginas, salvo la portada.

## Datos que pueden quedar viejos
No aplica.
