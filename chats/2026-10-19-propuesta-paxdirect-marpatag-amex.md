# Propuesta PaxDirect para Marpatag (venta a Amex con cobro directo al pasajero)

- **Fecha:** 2026-10-19
- **Proyecto / cliente:** Softur — iTraffic, cliente Marpatag (cliente final de Marpatag: Amex)
- **Actualiza a:** No aplica (base: relevamiento "Relevamiento_Marpatag_Amex_Condiciones_Comerciales", v1.0 del 09/10/2026, en Google Docs)

## Objetivo
Armar un documento de propuesta para enviar a Marpatag, con capturas de cada módulo, sobre cómo se resuelve en iTraffic/Serenity la venta a Amex cobrando y facturando directo al pasajero, con un nombre para el proceso.

## Estado final
Terminado. `Trabajo/Entregables/Propuesta PaxDirect - Marpatag (marca Softur).docx` y `.pdf`, 5 páginas, marca Softur.

## Decisiones y por qué
- Nombre del proceso: **PaxDirect** — "cobro directo al pasajero con beneficio corporativo". `[decisión]` (la usuaria pidió inventar uno)
- Diseño funcional definido por la usuaria (simplifica el relevamiento): `[decisión]`
  - Clientes: nueva solapa **Beneficios Corporativos** (al lado de Comisiones) con % por tipo de producto. En la maqueta suma "Habilita PaxDirect", "Operador para ítem de beneficio" y vigencia/país/ciudad como en Comisiones (propuesta propia, a validar).
  - Reserva: tilde **Cobro y facturación al pasajero**. La reserva queda a nombre de Amex (no Consumidor Final como decía el relevamiento), así las estadísticas quedan en Amex.
  - Al guardar: ítem nuevo con el % según los servicios, **operador Amex**, venta 0 y costo = beneficio; se recalcula al cambiar servicios.
- Tipos de producto = tipos de ítem de la reserva (`Ts`): TR, HO, SE, EV, PA. `[código]`
- Ítem de beneficio propuesto como eventual (EV), a confirmar con el cliente. `[hipótesis]`
- Puntos a confirmar dejados en el documento: base sin impuestos, tipo de ítem, facturación consumidor final vs. factura A, alta de Amex como operador, nombres. `[decisión]`

## Archivos, tablas y objetos relevantes
- Softur.Serenity (sólo lectura, `git pull` previo): `[código]`
  - `Softur.Serene.Web/Modules/A_Maestros/Agencia/AgenciaForm.generated.cs` — solapas del cliente: Generales, Vencimientos, Limites de Compra, Comisiones (`AgenciacomisionEditor`), Agenciaf8001, Agenciaib, Logo, Textgen, Observaciones, Centros de costos.
  - `A_Maestros/Agenciacomision/AgenciacomisionForm.generated.cs` — comisión por Centrocosto, Porc_comision, Fec_desde/hasta, Idpaises, Idciudades.
  - `E_Ventas/Reserva/ReservaForm.generated.cs` — categorías Encabezado, Detalle, Datos de Facturación (Cuitfacrva, Nombrefacrva, Direccionfacrva), Cliente secundario (`Cod_agcia2`).
  - `E_Ventas/Reserva/ReservaEndpoint.generated.cs` — tipos de ítem SE/HO/TR/PA/EV; setting `IT_USEFECINCOTI` (comisión por centro de costo).
  - Rutas: `A_Maestros/Agencia` (Clientes y Agencias), `E_Ventas/Reserva`.
- Entorno usado para relevar pantallas: iTraffic Caracol test (`test.ringo.softur.com.ar/iTraffic_Caracol`). `[datos]`

## Cambios hechos
- Se creó el .docx/.pdf en Entregables, reutilizando el paquete OOXML del alta IT Total (estilos, encabezado, pie, logo).
- No se modificó nada en Caracol test (las capturas son maquetas, no se guardó ningún dato) ni en Softur.Serenity.

## Errores y cómo se resolvieron
- Google Doc pedía login — la usuaria inició sesión en el navegador integrado; el texto se leyó desde la vista `/mobilebasic` (el editor dibuja en canvas).
- El panel del navegador integrado es chico y las capturas salían en baja resolución — se armaron maquetas HTML con las mismas hojas de estilo de Serenity del servidor (`<base href>` al sitio) y se renderizaron con **Edge headless** (`msedge --headless=new --force-device-scale-factor=2 --virtual-time-budget=8000 --screenshot`). Sin `--virtual-time-budget` el texto sale vacío (fuentes web); los íconos font-awesome no cargan desde `file://`, se reemplazaron por texto.
- En PowerShell no nombrar funciones `H` (alias de Get-History) ni variables `$pid` (de sólo lectura).

## Riesgos
- Las capturas son maquetas con datos de ejemplo (AMEX, Hotel Ejemplo, AX1027): la pantalla final puede variar en el desarrollo. `[hipótesis]`
- La propuesta difiere del relevamiento en el cliente de la reserva (Amex en vez de Consumidor Final); si Marpatag necesita la cuenta corriente a nombre del pasajero, hay que revisar. `[hipótesis]`

## Pendientes
- [ ] Enviar la propuesta a Marpatag y validar los 5 puntos de la sección 06 — usuaria.
- [ ] Con la validación, estimar horas de desarrollo — Softur.

## Cómo validar
1. Abrir el PDF: 5 páginas; portada "PaxDirect"; secciones 01–06; figuras 1 (solapa cliente), 2 (tilde reserva) y 3 (ítem 004 operador AMEX).
2. Ejemplo de cálculo: 20.000×10% + 10.000×15% + 4.000×15% = 4.100.

## Datos que pueden quedar viejos
- % de ejemplo de la maqueta (TR 5, HO 10, SE 15, EV 8, PA 12) — ilustrativos — (foto al 2026-10-19)
