# Correo de entrega de la Interfaz Caja de Hoteles a Eurovips

- **Fecha:** 2026-11-19
- **Proyecto / cliente:** Eurovips — Interfaz Caja de Hoteles (API Drawbridge)
- **Actualiza a:** [2026-11-18-comprobante-entrega-caja-hoteles-eurovips-parte-2.md](2026-11-18-comprobante-entrega-caja-hoteles-eurovips-parte-2.md)

## Objetivo
Redactar el correo que acompaña el comprobante de entrega (PDF) de la Interfaz Caja de Hoteles.

## Estado final
Terminado: correo redactado en el chat, listo para que la usuaria lo envíe con el PDF adjunto.

## Decisiones y por qué
- El correo informa que el desarrollo está listo y apto para pruebas en el ambiente de test (drawbridge-test). [decisión]
- Se recuerda lo ya informado por Yandy: aunque el ambiente es de test, las credenciales de Red Turística serían de producción, por lo que las reservas de prueba podrían ser reales; se pide cuidado (preferir búsquedas, cancelar en el momento lo que se reserve, coordinar antes). [decisión] Que las credenciales sean de producción se dice como "entendemos". [hipótesis]
- El pase a producción se coordina una vez validados los flujos, con la API key de producción (como dice el comprobante). [decisión]

## Archivos, tablas y objetos relevantes
- `CLIENTES/EUROVIPS/Comprobante de entrega - Interfaz Caja de Hoteles - Eurovips.pdf` (2 páginas, fecha 18/11/2026).
- No se consultó Softur.Serenity (el conector no está en ese repo).

## Cambios hechos
- Redacción del correo (no se generó archivo).

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Reservas de prueba confirmadas contra Red Turística con credenciales de producción pueden generar reservas reales o gastos.

## Pendientes
- [ ] Enviar el correo con el comprobante — usuaria.

## Cómo validar
- Revisar que el correo coincida con el comprobante: 4 métodos (SEARCH, BOOKING, GETBOOKING, CANCEL), ambiente testing, alcance sólo Hoteles.

## Datos que pueden quedar viejos
- Ambiente de la entrega — testing (drawbridge-test) — (foto al 2026-11-19)
- Credenciales de Red Turística — de producción, según lo informado por Yandy — (foto al 2026-11-19)
