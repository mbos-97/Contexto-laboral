# Minuta de Cuenta Corriente de Eurovips en tabla para pegar en el mail

- **Fecha:** 2026-11-04
- **Proyecto / cliente:** Eurovips (módulo Cuenta Corriente)
- **Actualiza a:** [2026-11-04-minuta-primera-entrega-cuenta-corriente-eurovips.md](2026-11-04-minuta-primera-entrega-cuenta-corriente-eurovips.md)

## Objetivo
Evitar que la tabla de la minuta se deforme al copiarla del chat al mail.

## Estado final
Terminado. Minuta en HTML y copiada al portapapeles con formato. El resultado pegado en el programa de correo no se comprobó.

## Decisiones y por qué
- Los puntos contemplados quedan en blanco en la columna "Diseño original" — pedido de la usuaria. [decisión]
- Tablas para mail: HTML con estilos en línea y copia con `Set-Clipboard -AsHtml` desde `powershell.exe` 5.1 con `-STA` — la tabla del chat se deforma al pegarla. [datos]

## Archivos, tablas y objetos relevantes
- `Entregables/Minuta - Primera entrega Cuenta Corriente Eurovips.html`

## Cambios hechos
Se creó el HTML y se copió su contenido al portapapeles.

## Errores y cómo se resolvieron
- Tabla deformada al pegarla desde el chat — se copia como HTML — se generó la versión anterior.

## Riesgos
El portapapeles se pisa con cualquier otra copia; se puede volver a copiar desde el HTML abierto en el navegador.

## Pendientes
- [ ] Revisar el pegado y enviar la minuta — usuaria.

## Cómo validar
Pegar en un mail nuevo y comprobar las cinco columnas y los nueve puntos.

## Datos que pueden quedar viejos
No aplica.
