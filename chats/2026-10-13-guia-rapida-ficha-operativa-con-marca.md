# Guía rápida de Ficha Operativa con identidad Softur

- **Fecha:** 2026-10-13
- **Proyecto / cliente:** Softur — material de usuario (iTraffic / Receptivo)
- **Actualiza a:** No aplica

## Objetivo
Convertir el instructivo "Ficha operativa para uso receptivo" (Word largo, redactado en prosa) en una guía simple de cara al usuario, sin la información no relevante y con color y tipografía del manual de marca.

## Estado final
Terminado. Se entregó `Ficha operativa - Guia rapida.docx` (4 páginas A4, editable) en la carpeta `Trabajo`.

## Decisiones y por qué
- Se quitó toda la parte de configuración previa (crear el operador/prestador "A designar", crear servicios, cargar tarifas, tomar el servicio en la reserva) y la explicación conceptual. Quedó resumida en un recuadro "Antes de empezar" de dos líneas, porque el usuario operativo sólo necesita saber que el servicio llega con prestador "A designar". `[decisión]` (criterio propio; la usuaria pidió "sacar lo no relevante" sin detallar qué)
- Estructura en 7 pasos numerados: buscar servicios del día, juntar reservas del mismo servicio, seleccionar y cargar hora, crear planning, revisar resultado, agregar/quitar reservas, colores y guías. `[decisión]`
- De 26 capturas se conservaron 6 (una por paso) más 3 íconos en línea. `[decisión]`
- Redacción en voseo y frases cortas, como pide el manual de marca (sección Voz). `[decisión]`
- Identidad aplicada según el manual "Softur. Sistema de marca y producto" v1.0.0 (16/09/2026): `[datos]`
  - Colores: Marfil `#FAF8F4` (fondo), Tinta `#191917` (texto), Naranja `#E66B24` (señal gráfica), Terracota `#B7470D` (acento con texto), Arena `#F0ECE5` (recuadros), separador `#DDD6CC`, texto secundario `#655F57` (muestreado del PDF).
  - Tipografías: DM Serif Display sólo para el título (≥ 28 pt); DM Sans para todo lo demás. Alternativas del manual: Georgia y Arial.
  - Documentos A4: márgenes 20 mm, cuerpo 11 pt, encabezado simple, secciones numeradas, pie con página.
  - Logo: no se redibuja. Se usó el PNG original sobre Tinta, recortado de la página 4 del manual.
  - No usar texto blanco chico sobre Naranja; para texto de acento va Terracota.
- Nombre del producto en el documento: "iTraffic / Receptivo" (es lo que muestran las pantallas y lo que el manual pide respetar). `[datos]`

## Archivos, tablas y objetos relevantes
- Origen: `FICHA OPERATIVA PARA USO RECEPTIVO (1).docx` y `manual-softur (2) (2).pdf` (en Descargas).
- Resultado: `Trabajo/Ficha operativa - Guia rapida.docx`.
- Softur.Serenity consultado (sólo lectura, con `git pull` previo) para validar nombres de pantalla: `[código]`
  - `Softur.Serene.Web/Modules/J_Receptivo/FichaOperativa/FichaOperativaGrid.ts` — botones "Nuevo Planning", "Salvar los Cambios", "Cerrar Ficha"; tooltips de búsqueda y filtros.
  - `Softur.Serene.Web/Modules/Texts.cs` — textos: sin hora no se puede hacer planning; botones "Asocia los elementos seleccionados a un planning existente" y "Quita los elementos seleccionados de su planning"; no se puede desasociar de un planning cerrado.
  - `Softur.Serene.Web/Common/Navigation/NavigationItems.cs` — menú Receptivo > Ficha Operativa; existe "Configuraciones > Columnas Ficha Operativa" (las columnas son configurables).
  - `J_Receptivo/Bloqueo/BloqueoRow.cs` — el planning es la entidad Bloqueo (campos Idvehiculo, Idchofer, Horadesde, Horahasta); `FichaOperativaRow.cs` — columnas Hora, Itinerario, Guia, Planning (`idbloqueo`).

## Cambios hechos
- Se creó el .docx nuevo. No se modificó el instructivo original ni el repo Softur.Serenity.

## Errores y cómo se resolvieron
- La PC no tiene Python, Node, pandoc ni poppler — el .docx se armó escribiendo el OOXML desde PowerShell 7 y empaquetando con `System.IO.Compression`.
- No se podía leer el PDF del manual (falta `pdftoppm`) — se renderizó cada página a PNG con `Windows.Data.Pdf` (WinRT) desde `powershell.exe` 5.1.
- Para revisar el resultado: Word por COM (`Documents.Open` + `ExportAsFixedFormat`) a PDF y de ahí a PNG con el mismo método.
- Saltos de página cortaban un paso por la mitad — se puso "conservar con el siguiente" en los párrafos de cada paso.

## Riesgos
- Las capturas muestran nombres de pasajeros, vendedor y chofer del entorno donde se tomaron. Si el documento va a clientes, conviene confirmar que son datos de prueba o reemplazar las capturas. `[hipótesis]`
- Las opciones de Estado del planning (Edita costeo y prestador, Recosteo directo, Asigno vehículo, Cerrado) se tomaron del instructivo original; no se encontraron como texto fijo en el código (vienen de datos). `[hipótesis]`
- Las fuentes DM Sans y DM Serif Display se ven bien en Word de esta PC; en una PC que no las tenga, Word usa Arial y Georgia. Para compartir fuera, exportar a PDF.

## Pendientes
- [ ] Confirmar con la usuaria si quiere recuperar algo de la parte de configuración que se quitó.
- [ ] Definir si las capturas se reemplazan por otras con datos de prueba.

## Cómo validar
1. Abrir el .docx en Word: 4 páginas, fondo marfil, título en serif, pasos 01 a 07.
2. Seguir los pasos en un entorno de prueba de iTraffic y comprobar que los nombres de botones y columnas coinciden.

## Datos que pueden quedar viejos
- Manual de marca — versión "Propuesta 1.0.0" — (foto al 2026-10-13)
- Nombres de botones y columnas de la Ficha Operativa — según el código al 2026-10-13
