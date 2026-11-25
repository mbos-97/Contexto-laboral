# Pedido de textos en inglés de Latitud: capturas del itinerario con referencias

- **Fecha:** 2026-11-25
- **Proyecto / cliente:** Latitud Ushuaia (código 05071)
- **Actualiza a:** [2026-11-25-pedido-textos-itinerario-ingles-latitud-ushuaia.md](2026-11-25-pedido-textos-itinerario-ingles-latitud-ushuaia.md)

## Objetivo
Sumar al pedido capturas del itinerario con números de referencia, como guía de dónde se ve cada texto.

## Estado final
Terminado. Mismo archivo en `Entregables` (`Pedido de textos del itinerario en ingles - Latitud Ushuaia (marca Softur).docx` / `.pdf`), sigue en 3 páginas.

## Decisiones y por qué
- Dos figuras en la página 1, debajo de "Cómo completar": Figura 1 (bienvenida, título y un servicio; ref. 1 a 3) y Figura 2 (guía, reseñas y cierre; ref. 4 a 8). [decisión]
- Cada fila de las tablas lleva en naranja su número de referencia antes del rótulo; Alojamiento y la leyenda de restricciones se marcan "no visible en la figura" (no aparecen en la reserva de prueba). [decisión]
- El nombre del pasajero se reemplazó por "NOMBRE DEL PASAJERO" en la captura. [decisión]
- El recuadro "A tener en cuenta" pasó a ser el paso 4 de "Cómo completar" para que las figuras entren en la página 1. [decisión]

## Archivos, tablas y objetos relevantes
- Captura de la reserva id 54119 (`lang=es`).

## Cambios hechos
- Se regeneraron el .docx y el .pdf con las dos figuras y las referencias.

## Errores y cómo se resolvieron
- El .docx estaba abierto en Word y no se podía pisar — se generó con otro nombre y se renombró al cerrarse.
- Capturas: el HTML del itinerario se arma en el servidor; se bajó con `curl`, se le agregaron `<base href>`, CSS y círculos numerados, y se capturó con Chrome headless (`--screenshot`, `--force-device-scale-factor=2`); el recorte del blanco se hizo con System.Drawing en pwsh. Hay que ocultar el botón flotante (`.model-2`, `.back-to-top`).

## Riesgos
- Las figuras son chicas (≈4,6 cm de ancho); se leen los números, el texto fino del itinerario no tanto.

## Pendientes
- [ ] Enviar el pedido a Latitud (sigue el pendiente de la memoria anterior) — usuaria.

## Cómo validar
1. Abrir el .pdf: 3 páginas, figuras en la página 1 con círculos 1 a 8 y números naranjas en las filas.

## Datos que pueden quedar viejos
- Reserva usada para las capturas — id 54119 — (foto al 2026-11-25)
