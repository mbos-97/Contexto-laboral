# Circuito de viáticos de choferes (pago previo al viaje) con autorización de pago

- **Fecha:** 2026-11-06
- **Proyecto / cliente:** Softur — iTraffic (caso de choferes, probablemente Cuenca del Plata; no confirmado)
- **Actualiza a:** No aplica. Relacionado con [2026-10-30-validacion-circuito-precompra-entradas.md](2026-10-30-validacion-circuito-precompra-entradas.md)

## Objetivo
Explicar brevemente, para un correo, el circuito de aprobación de viáticos de choferes que se entregan antes del viaje, y resolver la duda: la autorización sin imputar no tiene operador real y la autorización de pago no tiene reimputación.

## Estado final
Terminado: respondido en el chat con texto para el correo y propuesta.

## Decisiones y por qué
- La reimputación existe sobre la **OP**, no sobre la autorización: Proveedores › Reimputación OP toma el saldo de una OP y lo aplica a ítems de reserva. `[código]`
- Propuesta: los viáticos se cargan en la reserva con un prestador/operador "Viáticos choferes" (o un operador por chofer). Si el costo ya está en la reserva antes del viaje, la autorización se imputa directo a la reserva y no hace falta reimputar. Si se entrega un anticipo antes de tener el costo, la autorización sin imputar sale a **ese mismo operador**, Tesorería saca la OP (queda saldo a favor) y al costear se aplica con Reimputación OP. `[hipótesis]` (validar en base de prueba)
- Alternativa contable si se quiere separar el anticipo: mismo esquema que precompra de entradas (cuenta Anticipo viáticos). `[hipótesis]`

## Archivos, tablas y objetos relevantes (Softur.Serenity)
- `Softur.Serene/Softur.Serene.Web/Modules/G_Proveedores/ReimputacionOP/ReimputacionOPDialog.ts` (`ReimputarOp`, picker de OP con `tipocc` 7, detalle con `tipocc` 8)
- `Softur.Serene/Softur.Serene.Web/Modules/G_Proveedores/Ordenpag/OrdenpagEndpoint.generated.cs` (`ReimputarOp`)
- `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/iLSALDPROV_ForOPA_FPP_Itraffic.sql` (`tipocc` 8: saldos por reserva / OP / mov_ord)
- Tablas: `Autoriza`, `Ordenpag`, `Mov_ord`, `Imputaci`, `Operador`

## Cambios hechos
No aplica (sólo respuesta).

## Errores y cómo se resolvieron
No aplica.

## Riesgos
- Si el operador de la autorización/OP no es el mismo que el del costo en la reserva, la Reimputación OP no va a encontrar los ítems (filtra por operador). `[hipótesis]`
- Diferencias entre lo entregado y lo rendido quedan como saldo del operador si no se define regla (devolución o pago de diferencia).

## Pendientes
- [ ] Probar en base de prueba: AUT sin imputar → OP → Reimputación OP contra los ítems de viáticos de la reserva, con el mismo operador — usuaria.
- [ ] Definir si se usa un operador genérico "Viáticos choferes" o uno por chofer — cliente.

## Cómo validar
Generar AUT sin imputar a "Viáticos choferes", sacar la OP, cargar el costo en la reserva con prestador de ese operador y abrir Reimputación OP: la OP debe aparecer con saldo y permitir imputarla a la reserva.

## Datos que pueden quedar viejos
No aplica.
