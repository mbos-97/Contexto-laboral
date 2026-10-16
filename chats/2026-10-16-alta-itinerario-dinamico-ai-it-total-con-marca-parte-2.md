# Comprobante de alta del Itinerario Day by Day (AI): puntos 1 a 10 y apartado General

- **Fecha:** 2026-10-16
- **Proyecto / cliente:** Softur — alta de producto Itinerario dinámico Day by Day (`Travel.Itinerary.AI`), cliente Destinos Australes
- **Actualiza a:** [2026-10-16-alta-itinerario-dinamico-ai-it-total-con-marca.md](2026-10-16-alta-itinerario-dinamico-ai-it-total-con-marca.md)

## Objetivo
Rehacer el comprobante con las capturas y la numeración que armó la usuaria, y con los pedidos de información que definió para cada punto.

## Estado final
Terminado. `Trabajo/Entregables/Alta Itinerario dinamico AI - IT Total (marca Softur).docx` y `.pdf` (7 páginas), con el mismo nombre de archivo. La versión que devolvió la usuaria quedó como respaldo sólo en el scratchpad de la sesión.

## Decisiones y por qué
- Portada según la usuaria: título "Itinerario dinámico Day by Day", producto "Itinerario day by day", fecha de envío 16-10-2026 y nuevo texto en "Importante" (una única instancia de ajustes). `[decisión]`
- Se usan las capturas de la usuaria (números rojos), una debajo de la otra, al inicio de la sección 01. `[decisión]`
- Numeración 1 a 10: la imagen original repetía el 7 en "End of your services"; con su OK se corrigieron los números de la última captura (fin de servicios 8, términos 9, pie 10). `[decisión]`
- Puntos `[decisión]` (definidos por la usuaria):
  1. imagen de portada;
  2. texto antes del nombre del pasajero;
  3. título y columnas visibles del resumen de cotización;
  4. título y columnas del detalle de pasajeros;
  5. información importante o recomendaciones (título y cuerpo);
  6. texto de bienvenida (título y cuerpo);
  7. textos del servicio: campos nuevos o un campo existente (indicar cuál);
  8. leyenda de fin de servicios;
  9. términos y condiciones (título y cuerpo);
  10. contacto y pie.
- Apartado "02 General": tipografía, color de los fondos de texto y color de la tipografía. `[decisión]`
- Se quitaron las secciones aparte "Lo que se carga en iTraffic" y el checklist. Lo que sale del sistema se indica dentro de cada punto con la etiqueta "SE CARGA EN iTRAFFIC". `[decisión]`
- Punto 7: hoy el título del día es la descripción del servicio en la reserva y el descriptivo sale de `det_rvait` (textos del servicio, p. ej. "Título IT" 72 / "Detalle IT" 74); para servicios hay también un texto corto por idioma (códigos 84 ESPA, 80 INGL, 86 ALEM). `[código]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity (sólo lectura): `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/iDet_rvait_SelectBooking.sql` — campos `Titulo`, `descripcion`, `Descripciondetallada`, `descripcioncorta` (textgen `SERVICIO` 84/80/86). `[código]`

## Cambios hechos
- Se regeneró el .docx y el PDF en `Entregables`. Los números de dos capturas se repintaron con C# `System.Drawing`.

## Errores y cómo se resolvieron
- Numeración inconsistente entre las imágenes y el mensaje — se le consultó a la usuaria y se unificó en 1 a 10.

## Riesgos
- Si la usuaria tenía cambios propios en el Word que no eran imágenes ni portada, se perdieron en el archivo de Entregables (el respaldo quedó en el scratchpad de la sesión). `[hipótesis]`

## Pendientes
- [ ] Confirmar si el nombre del archivo debe cambiar a "Day by Day - Destinos Australes".

## Cómo validar
1. Abrir el PDF: 7 páginas; las imágenes van del 1 al 10 sin repetir números; la sección 02 se llama "General".

## Datos que pueden quedar viejos
- Código de cliente Destinos Australes — 00336 — (foto al 2026-10-16)
