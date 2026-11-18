# Planilla "Información a cargar · Tarifario Web" para Tolkeyen (marca Softur)

- **Fecha:** 2026-11-17
- **Proyecto / cliente:** Tolkeyen — Tarifario Web (PriceList)
- **Actualiza a:** No aplica (relacionada con [2026-11-17-manual-tarifario-web-v1-parte-2.md](2026-11-17-manual-tarifario-web-v1-parte-2.md))

## Objetivo
Pasar a la marca Softur (logo, colores y tipografía) el Excel de control "INFORMACION A CARGAR TARIFARIO WEB", sumar el logo de Tolkeyen y agregar una solapa GENERALES.

## Estado final
Terminado: `Entregables/Informacion a cargar - Tarifario Web - Tolkeyen (marca Softur).xlsx`. Solapas: GENERALES (nueva), DESTINOS, Ushuaia, Calafate, Patagonia Chilena. No se modificó el original en Descargas.

## Decisiones y por qué
- Solapa GENERALES, primera, con 4 tareas y casilla "Completo" + "Observaciones": Carga de contacto de clientes, Carga de logo en ABM Cliente, Carga de imágenes en destino (home), Carga de imágenes de productos por destino. Pedido de la usuaria. [decisión]
- Encabezado de cada solapa: banda Tinta con el logo Softur a la izquierda; título "Información a cargar · Tarifario Web" en DM Serif Display sobre Marfil, subtítulo (destino o "Resumen de avance por destino") en DM Sans gris, línea Naranja. El logo de Tolkeyen (SVG, azul y rojo) va sobre Marfil a la derecha, no sobre la banda negra, porque no se lee sobre Tinta. [decisión]
- Tablas: encabezado de sección en Tinta con texto blanco, encabezados de columna en Arena, "Completos" de DESTINOS en Naranja, bordes `#DDD6CC`, sin líneas de cuadrícula; contenido original (títulos, columnas, destinos) sin cambios. [decisión]
- Los FALSE del original (casillas de Google Sheets que Excel muestra como texto) se convirtieron en casillas de verificación nativas de Excel, en color Naranja. [decisión]

## Archivos, tablas y objetos relevantes
- Original: `Downloads/INFORMACION A CARGAR TARIFARIO WEB .xlsx` (exportado de Google Sheets, Raleway, sin fórmulas ni validaciones).
- Logo Tolkeyen: `Downloads/tolkeyen-logo (2).svg` (incrustado como SVG).
- Logo Softur: `word/media/image1.png` de `Entregables/Circuito sugerido para empresas receptivas (marca Softur).docx` (PNG 990×396 con fondo Tinta).
- Softur.Serenity: no se consultó (tarea de formato).

## Cambios hechos
- Se creó el .xlsx con Excel por COM desde PowerShell (no hay Python en la máquina) y luego se agregó por XML el soporte de casillas.

## Errores y cómo se resolvieron
- En PowerShell las variables no distinguen mayúsculas: `$x` pisó a `$X` (ruta) — se renombró la variable. [datos]
- Casillas de verificación de Excel: se agregan a mano con `xl/featurePropertyBag/featurePropertyBag.xml` (bags Checkbox → XFControls → XFComplement → XFComplements), relación `http://schemas.microsoft.com/office/2022/11/relationships/FeaturePropertyBag`, content type `application/vnd.ms-excel.featurepropertybag+xml` y, en cada `xf` de las celdas booleanas, `<extLst><ext uri="{C7286773-470A-42A8-94C5-96B5CB345126}"><xfpb:xfComplement i="0"/></ext></extLst>`. Excel (build 20527) lo abrió y lo conservó al guardar. [datos]
- Vista previa: Excel exporta a PDF por COM y `Windows.Data.Pdf` (powershell.exe 5.1) lo pasa a PNG; el Read de PDF no funciona sin poppler. [datos]

## Riesgos
- DM Sans / DM Serif Display son fuentes de nube de Office: en un equipo sin ellas Excel las reemplaza. En Google Sheets o Excel viejos las casillas se ven como VERDADERO/FALSO. [hipótesis]

## Pendientes
- No aplica.

## Cómo validar
- Abrir el .xlsx en Excel 365: 5 solapas, logos Softur y Tolkeyen en cada una, casillas clickeables en Naranja.

## Datos que pueden quedar viejos
- Destinos de la planilla — Ushuaia, Calafate, Patagonia Chilena (foto al 2026-11-17).
