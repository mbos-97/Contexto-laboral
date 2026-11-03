# Notas de reunión del portal de agencias Eurovips

- **Fecha:** 2026-11-03
- **Proyecto / cliente:** Eurovips (portal de agencias, Reservas y Cobranza)
- **Actualiza a:** No aplica

## Objetivo
Armar una minuta para enviar por mail a partir de notas en papel de una reunión.

## Estado final
Parcial. Se hizo un borrador de minuta, pero la usuaria prefirió armarla por su cuenta y pidió sólo la transcripción de las notas. La minuta final y el envío quedan de su lado.

## Decisiones y por qué
- La usuaria redacta la minuta — el borrador no le sirvió. [decisión]

## Archivos, tablas y objetos relevantes
- Portal: `eurovips.itraffic.com.ar/iTraffic_Eurovips.Giata.SAA`. Usa endpoints Umbraco `umbraco/Surface/Booking/...` (`HandleRequestContactNotification`, `HandleInvoiceRequest`). [datos]
- Softur.Serenity: búsqueda de textos del portal en `Softur.Serene.Web/Modules` y `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD`, sin resultados: el portal no parece estar en ese repo. [hipótesis]
- Softur.Serenity: `Softur.Serene.Model/Modules/L_Configuraciones/Entities/TextgenRow.cs`, tabla `Textgen` (`Codigotext`, `Valortext`, `Tablatextgen`, `Idtablatextgen`); `A_Maestros.AgenciaForm.ts` tiene el editor Textgen. [código]
- Pantallas vistas: Inicio, Reservas, Pagos / Solicitar (figura como demo), Cuentas bancarias, Contacto, Datos Agencia. [datos]

## Cambios hechos
Ninguno en el portal ni en Softur.Serenity (sólo lectura).

## Errores y cómo se resolvieron
No aplica.

## Riesgos
Las notas tienen partes dudosas; su interpretación no está confirmada. [hipótesis]

## Pendientes
- [ ] Armar y enviar la minuta — usuaria.

## Cómo validar
No aplica.

## Datos que pueden quedar viejos
- Usuario revisado GIATA.SAA: "Datos Agencia" sin CUIT, dirección ni teléfono, y "Contacto" vacío — (foto al 2026-11-03)
