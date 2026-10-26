# Minuta de relevamiento Cuenca del Plata: todos los sectores, ordenada para implementar

- **Fecha:** 2026-10-26
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria.md](2026-10-26-minuta-relevamiento-cuenca-del-plata-tesoreria.md)

## Objetivo
Ordenar la minuta completa por sector (cómo trabaja hoy, problemáticas, objetivos) para arrancar la implementación con los equipos el 2026-10-27.

## Estado final
Terminado. `Trabajo/Entregables/Minuta de relevamiento - Cuenca del Plata (marca Softur).docx` (+ `.pdf`), 7 páginas: portada con mapa de sectores y una página por sector.

## Decisiones y por qué
- Orden de los sectores según el circuito (como en el circuito operativo del 2026-10-15): 01 Reservas, 02 Operaciones, 03 Proveedores, 04 Tesorería, 05 Administración, 06 Puntos a confirmar. Cada uno con Equipo, Cómo trabaja hoy, Problemáticas y Objetivos. `[decisión]`
- Lo relevado: `[decisión]` (dicho por el cliente)
  - **Reservas:** las reservas que no son de grupos se cargan como paquetes de servicio (sin problemas); eventuales sólo para grupos; los errores de tarifa hotelera van Proveedores → Reservas → Cargas. Problemas: multihotel en grupos, nominación por servicio, productos muy vendidos sin cargar. Objetivos: normalizar la carga, reducir eventuales, nombre de grupo, estado "Falta vuelo" revisado antes del fin de semana, adicionales que piden los guías (con productos "extra guía" y "extra transporte"), guía como ítem en seriados, opcionales asociados a la reserva principal.
  - **Operaciones:** todo gasto en el planning. Problemas: vehículos propios ociosos mientras se contrata a terceros, choferes sin orden de servicio, multihotel que no figura, opcionales sin asociar, 2-3 guías por vehículo que la orden de servicio no muestra, guías que no usan Mobile. Objetivos: sin orden de servicio no sale el chofer; Operaciones carga el planning y Comercial costea los servicios de terceros 1 día después de prestados; los extras se cargan como ítem extra del planning y Comercial ajusta el costo; asignación de guías centralizada en la responsable de guías; grilla de servicios con y sin planning; excluir del planning lo que no se opera (línea de paquete, hotelería, agua, propina, presente, pilotín); paquetes de servicio con traslado de ida y vuelta.
  - **Proveedores:** hoteles se pagan contra proforma (costo de la proforma, no del file); transporte se autoriza contra orden de servicio; la importación de facturas es una macro sin imputación a planning ni reserva. Objetivos: autorización de pagos (solicitud + comprobante), autorizar sólo el costo que está en el file, file bloqueado después de la autorización de pago, número de planning en cada comprobante, corregir la importación, ver en la ficha operativa qué servicios se hicieron, operador interno que ingresó la contratación extra en la orden de servicio.
  - **Tesorería:** sin cambios respecto de la memoria anterior; se agregan las reservas incompletas como problema.
  - **Administración:** imputación de cobros; control de cuentas corrientes 96 h antes del ingreso del pasajero para dar el servicio o cancelarlo.
- Contradicción marcada para confirmar: Proveedores dijo que el costo lo carga Operaciones; Operaciones acordó que Comercial genera el costeo de servicios de terceros. `[hipótesis]`
- Otros puntos abiertos: categoría por vehículo en privados, guardia manual vs. importación de files extras para opcionales, responsable de los pagos de servicios, nombres repetidos entre equipos. `[hipótesis]`

## Archivos, tablas y objetos relevantes
- Generador: `minuta.ps1` + `contenido.ps1` (scratchpad de la sesión), sobre la plantilla OOXML de la marca Softur.
- Softur.Serenity: no se consultó (se transcribe lo que dijo el cliente, sin afirmaciones del sistema).

## Cambios hechos
- Se reemplazó el .docx/.pdf de la minuta (antes sólo Tesorería, 2 páginas) por la versión completa de 7 páginas.

## Errores y cómo se resolvieron
- Operaciones se pasaba de página — se unieron las dos listas de problemáticas (indicando "otros sectores") y "normalizar la carga" pasó a los objetivos de Reservas.

## Riesgos
- Los nombres de las personas salen de la minuta; puede haber homónimos o apodos (Romina/Romi, Marcelo en dos sectores). `[hipótesis]`

## Pendientes
- [ ] Confirmar con Cuenca del Plata los 5 puntos de la sección 06 — usuaria — 2026-10-27.

## Cómo validar
1. Abrir el PDF: 7 páginas; portada con mapa de sectores 01–06; cada sector en su propia página.

## Datos que pueden quedar viejos
- Equipos por sector y objetivos "de esta semana" — (foto al 2026-10-26)
