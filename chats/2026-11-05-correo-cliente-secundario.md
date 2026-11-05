# Correo al cliente: cómo funciona el cliente secundario

- **Fecha:** 2026-11-05
- **Proyecto / cliente:** No indicado
- **Actualiza a:** [2026-11-04-cliente-secundario-reserva-parte-2.md](2026-11-04-cliente-secundario-reserva-parte-2.md)

## Objetivo
Explicar en lenguaje simple al cliente cómo funciona el cliente secundario en reserva, factura y recibo.

## Estado final
Terminado: borrador de correo entregado en el chat, para que lo envíe la usuaria.

## Decisiones y por qué
- Mensaje central: el secundario aporta los datos fiscales de la factura; deuda y pagos quedan en el principal. [código]
- Sin nombres de configuraciones ni excepciones técnicas (recargos, datos del pasajero), para que el cliente lo entienda fácil. [decisión]
- Se ofrecen dos salidas: cargar al secundario como principal, o relevar y cotizar un desarrollo. [hipótesis]

## Archivos, tablas y objetos relevantes
Basado en las memorias de 2026-11-04 sobre cliente secundario. No se volvió a leer Softur.Serenity.

## Cambios hechos
No aplica.

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Si la instalación del cliente no tiene activa la facturación con datos del secundario (`lfacagciados`), la factura sale con los datos del principal. Conviene confirmarlo antes de enviar. [hipótesis]

## Pendientes
- [ ] Confirmar `lfacagciados` en la base del cliente antes de enviar — usuaria.

## Cómo validar
Comparar el correo con las memorias del 2026-11-04.

## Datos que pueden quedar viejos
No aplica.
