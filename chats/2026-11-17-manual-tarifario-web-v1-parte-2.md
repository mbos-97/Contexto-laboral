# Manual de uso Tarifario Web v1 genérico (marca Softur)

- **Fecha:** 2026-11-17
- **Actualiza a:** [2026-11-17-manual-tarifario-web-v1.md](2026-11-17-manual-tarifario-web-v1.md) (el PDF viejo decía que se mostraban las Observaciones; ya no es así)

## Estado final
Terminado: `Entregables/Manual de uso - Tarifario Web v1 (marca Softur).docx` + PDF, 12 páginas, 13 capturas. Las capturas del tarifario llevan números naranjas y las de iTRAFFIC, recuadros y letras rojas. Se ocultaron el logo y el nombre del cliente, el usuario y el pie con el nombre del receptivo. Relevado sobre el iTRAFFIC Tolkeyen y su PriceList (`itraffic.dyndns.org/iTraffic_Tolkeyen.PriceList/`). La usuaria inició sesión; no se guardaron credenciales.

## Qué se carga y dónde (verificado en pantalla y en los datos) `[datos]`
- **Logo del encabezado:** Maestros › Clientes › solapa **Logo** (`agencia.IMAGEN1`) del cliente del contacto logueado. Se muestra a 196×61 px; se recomienda PNG transparente de 400×125 px.
- **Imagen de cada destino (Inicio):** Maestros › Localización › Ciudades › solapa **Imágenes**, primera imagen (`ciudades.Imagenciudad`, devuelta por el SP `Ciudad_ListWeb`). El CSS es `background-size:auto; repeat`: se ve a tamaño real en una franja de 220 px de alto y se repite si es angosta. Referencia: 1920×220 px. Sin imagen, la franja queda naranja.
- **Imagen de cada categoría del destino** (Paquetes/Traslados/Excursiones/Hoteles): Configuraciones › **BannerPage** con `nombrepage = DEST`, país y ciudad del destino y Tipo Prestación S. La categoría sale del **nombre del banner** (PAQUETES / TRF / EXC / HOTEL), no del orden: se observó con "TRF USH" que va a Traslados aunque tenga orden 1. Sin banner aparece una imagen fija del sitio (`Agents/00197/images/...`). La tarjeta mide 350×320 px, con `cover` y centrado. Referencia: 1100×1000 px.
- **Resultados de servicio:** carrusel con Servicio › **Imágenes** (hasta 10, `IMAGENSERVICIOs`) y tarjeta de 350×320 px con `cover`. El nombre es la **Descripción** del servicio.
- **Ventana "Ver tarifas":** muestra textos de Servicio › **Textgen**: `T. WEB DESCRIPCION DE SERVICIO` (título), `T. WEB PROMOCIONES`, `T. WEB ACLARACION CAMBIO` (franja roja) y la tabla de tarifas (Categoría, Moneda, importe, CHD, Vigencia). La leyenda "Tarifas por pasajero sujetas a modificación…" es fija.
- **Botón "Ver detalles del descriptivo":** es un link cuyo href es el Textgen `T. WEB VER DETALLES DESCRIPTIVO` (código 61, `Tablatextgen = SERVICIO`). Si está vacío, el botón no aparece.
- Los demás T. WEB (duración, idioma, incluye, no incluye, importante, etc.) y la solapa **Observaciones** del servicio **no se ven** en las pantallas revisadas.
- La búsqueda de excursiones del PriceList puede tardar varios minutos o quedarse colgada; a veces devuelve `NO_RATES` hasta que cargan los combos.

## Softur.Serenity consultado `[código]`
- `Model/Modules/A_Maestros/Entities/CiudadesRow.generated.cs` (Imagenciudad 1-4), `AgenciaRow.generated.cs` / `ProvedorRow` (`IMAGEN1s`), `ServicioRow.generated.cs` (Imagenservicio 1-10).
- `Model/Modules/L_Configuraciones/Entities/BannerPageRow.generated.cs`, `Web/Modules/L_Configuraciones/BannerPage/BannerPageEndpoint.generated.cs` (servicio `Services/L_Configuraciones/BannerPage/List`), `Sp_Configs/BannerPageConfig.sql`.
- `ScriptsBD/Sp/Ciudad_ListWeb.sql` (configs `WEB_SOLODESTPUBLI`, `ORDNOMBRECIUTARIF`, `LIMPIAPAISNOPUBLICADO`).
- `Web/Modules/L_Configuraciones/Textgen/TextgenEndpoint.cs`.
- El código del PriceList (Umbraco) no está en Serenity.

## Cómo se hizo
- Capturas con el navegador integrado: sólo la pestaña activa toma el ancho del panel, y `zoom` devuelve hasta 800 px de ancho. Las marcas se dibujaron con C# `System.Drawing` (escala ×2) y el Word se armó reusando el paquete del manual iCONNECT, con los scripts `build_manual.ps1` y `annotate.ps1` en el scratchpad.
- Un `.ps1` con caracteres UTF-8 (›, ·) necesita BOM para `powershell.exe` 5.1; si no, falla el parseo. `[datos]`

## Pendientes
- [ ] Confirmar con desarrollo la regla del nombre del banner (PAQUETES/TRF/EXC/HOTEL) y si `Codigocliente` del BannerPage filtra por cliente.
- [ ] Confirmar dónde se usan los otros textos T. WEB (duración, idioma, incluye…) y las pantallas de Hoteles y Paquetes, que no se relevaron.
