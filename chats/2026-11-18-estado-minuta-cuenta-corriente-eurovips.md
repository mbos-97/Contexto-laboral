# Estado de la minuta de Cuenta Corriente de Eurovips

- **Fecha:** 2026-11-18
- **Proyecto / cliente:** Eurovips (módulo Cuenta Corriente)
- **Actualiza a:** [2026-11-04-minuta-primera-entrega-cuenta-corriente-eurovips.md](2026-11-04-minuta-primera-entrega-cuenta-corriente-eurovips.md)

## Objetivo
Actualizar la tabla de la minuta con el estado de cada punto.

## Estado final
Terminado. Tabla con columna "Estado", filas OK en verde y pendientes en amarillo, exportada como imagen.

## Decisiones y por qué
- Puntos 1, 3, 4, 6 y 7: OK. [decisión]
- Punto 2 (banner de imágenes en iTRAFFIC): pendiente de Softur. [decisión]
- Punto 5 (cuentas bancarias): se aguardan los datos actualizados de Damián; la parte de Softur sigue pendiente. "Pendiente de" pasa a "Eurovips (Damián) y Softur". [decisión]
- Puntos 8 y 9: se aguardan los archivos de referencia de Eurovips. [decisión]
- Imagen generada con Edge headless (`--screenshot`, escala 2) desde un HTML con estilos en línea. [datos]

## Archivos, tablas y objetos relevantes
- `Entregables/Minuta - Estado Cuenta Corriente Eurovips.html`
- `Entregables/Minuta - Estado Cuenta Corriente Eurovips.png`
- No se consultó Softur.Serenity (tarea de documento, sin lógica del sistema).

## Cambios hechos
Se crearon el HTML y la imagen PNG.

## Errores y cómo se resolvieron
- Espacio en blanco debajo de la tabla — alto de ventana excesivo — se ajustó `--window-size` a 1040x584.

## Riesgos
No aplica.

## Pendientes
- [ ] Punto 2: banner de imágenes en iTRAFFIC — Softur.
- [ ] Punto 5: datos de cuentas bancarias — Eurovips (Damián); luego Softur.
- [ ] Puntos 8 y 9: archivos de referencia (descarga Altair y formato de cuenta corriente) — Eurovips (Damián).

## Cómo validar
Abrir el PNG y comprobar las seis columnas, los nueve puntos y los colores por estado.

## Datos que pueden quedar viejos
- Estado de los puntos — 5 OK, 4 pendientes — (foto al 2026-11-18)
