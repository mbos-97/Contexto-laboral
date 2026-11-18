# Circuito sugerido para empresas receptivas (genérico, marca Softur)

- **Fecha:** 2026-11-16
- **Proyecto / cliente:** Softur — material genérico de implementación iTRAFFIC (receptivos)
- **Actualiza a:** [2026-11-16-proceso-administrativo-contable-trips-south-america.md](2026-11-16-proceso-administrativo-contable-trips-south-america.md)

## Objetivo
Rehacer el documento de TSA como material genérico, sin cliente: "Circuito sugerido para empresas receptivas", más fácil de leer para un cliente que no implementó, con el esquema primero, sin el resumen de etapas en la portada y con todo lo posible de iTRAFFIC (menús, estados, campos).

## Estado final
Terminado. `Trabajo/Entregables/Circuito sugerido para empresas receptivas (marca Softur).docx` (+ `.pdf`), 13 páginas: portada (título + "La idea en una frase") · El circuito en un vistazo (diagrama) · Conceptos clave + Quién hace qué · 01 Reserva · 02 Ficha operativa · 03 Planning · 04 Autorización de pago (4A/4B) · 05 Factura de proveedor (5A/5B) · 06 Orden de pago · 07 Cobro y factura al cliente · 08 Controles · Errores frecuentes. El documento de TSA quedó en Entregables sin tocar.

## Decisiones y por qué
- Genérico: sin nombre de cliente en portada, encabezado ni archivo. Pedido de la usuaria. `[decisión]`
- Estructura fija por sección: frase de qué es → ficha (Responsable / Dónde, en iTRAFFIC / Qué deja hecho) → pasos numerados → recuadro. Pensado para un cliente sin implementación. `[decisión]`
- Se suman un glosario (reserva, ítem, prestador, operador, ficha, planning, AUT, factura, OP, imputar) y una tabla de errores frecuentes. `[decisión]`
- No se incluyen anticipos (AUT sin imputar → OP → Reimputación OP) porque no está probado. `[decisión]`

## Archivos, tablas y objetos relevantes (Softur.Serenity)
- Menús (`NavigationLink`): Ventas › Alta Reserva (43), Ventas › Vencimientos Reserva (509), Clientes › Recibos (605), Clientes › Facturas (602), Proveedores › Autorización Pagos (702), Proveedores › Facturas Proveedores (703), Proveedores › Ordenes de Pago (705), Receptivo › Ficha Operativa (901), Reportes › SaldoProveedor_List / SaldoAutoriza_List / SaldoCliente_List. Los textos en pantalla pueden variar por traducción. `[código]`
- Estados del planning (`bloqueo.estado`, parámetro `ESVH`, `J_Receptivo/Bloqueo/ParamEstadoLoockupScript.cs`): A = AUTORIZAR PAGO, O = OK, R = RECOSTEO DIRECTO, C = CERRADO / COSTEO DIRECTO (según datos iniciales). En `iFichaopern_BloqueoAfterSave.sql`, con A genera las AUT y al terminar deja el planning en O "para que no vuelva a autorizar". `[código]`
- `G_Proveedores/Autoriza/AutorizaDialog.ts`: botón "Autorizar" sólo con permiso `G_Proveedores:Autoriza:PuedeAutorizar`; marca `Autorizada` y guarda el usuario en `Autorizado` ("Autorizó"). No se verificó si la OP exige AUT autorizada. `[código]`
- Resto igual que la memoria anterior (`iLSALDPROV_ForOPA_FPP_Itraffic.sql` "?nro", `iFacProv_AfterSave.sql` "PL").

## Cambios hechos
- Se crearon el .docx y el .pdf genéricos. Diagrama: "Reserva con costos y vencimientos" y "Planning en estado "Autorizar pago"".

## Errores y cómo se resolvieron
- `sed` con `\\n` en el reemplazo metió un salto de línea real dentro de un string C# — se corrigió con Edit.

## Riesgos
- Que el estado "Autorizar pago" y los nombres de menú cambien por traducción o datos del cliente. `[hipótesis]`
- La búsqueda "?nro de planning" en la factura de proveedor sigue sin probarse en pantalla. `[hipótesis]`

## Pendientes
- [ ] Probar en base de prueba "?nro de planning" al imputar factura de proveedor y si la OP pide la AUT marcada como Autorizada — implementación.

## Cómo validar
1. PDF de 13 páginas: portada sin tabla de etapas; página 2 con el diagrama; página 3 con conceptos y quién hace qué; ninguna mención a clientes.

## Datos que pueden quedar viejos
- Nombres de menú y estados de planning (dependen de traducciones y de la tabla `parame` de cada base).
