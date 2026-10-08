# Plan de cuentas: sin ciudades, bancos ni referencias a Bolivia

- **Fecha:** 2026-10-08
- **Proyecto / cliente:** Plan de cuentas de cliente agencia, para usar como plantilla genérica.
- **Actualiza a:** [2026-10-08-plan-de-cuentas-anonimizado.md](2026-10-08-plan-de-cuentas-anonimizado.md)

## Objetivo
Que el plan sea genérico y no se note que es de Bolivia: quitar ciudades, nombres de bancos y otras entidades bolivianas.

## Estado final
Terminado sobre `Descargas\PlandeCuentasList_20261008_104108_ajustado.xlsx`, que ahora queda con ambas rondas aplicadas. El original sigue intacto.

## Decisiones y por qué
- Ciudades → "Ciudad N": SRZ=1, LPB=2, CBB/CBBA=3, ORU=4, SRE=5, TJA=6. Las "Sucursal N" de la ronda anterior se mantienen dentro de cada ciudad. `[decisión]`
- Bancos → "Banco N" por orden de aparición: 1 Anchor Bank, 2 Bisa, 3 Santander, 4 BancoSol, 5 BCP, 6 BEC, 7 BMSC/Mercantil Santa Cruz, 8 BNB, 9 Brex, 10 FIE, 11 Ganadero, 12 LAFISE, 13 PRODEM, 14 Sabadell, 15 Unión. El mismo banco tiene siempre el mismo número. `[decisión]`
- Otras entidades bolivianas: `[decisión]`
  - "Esfuerzo por Bolivia" → "Segundo Aguinaldo"
  - "AFP Gestora" → "Fondo de Pensiones"
  - "Caja Nacional de Salud" → "Seguro de Salud"
  - Abavyt → "Asociacion de Agencias"
  - ECOJET y BOA → "Aerolinea"
  - ATC → "Procesador 1"; Linkser → "Procesador 2"
  - "Proyecto SIN" → "Proyecto Administracion Tributaria"
  - Autoridad de Fiscalización del Juego → "Tasa de Fiscalizacion de Juegos"
  - "GanaRendimiento F" → "Fondo de Inversion"
  - "Costa Rica" se quitó de "Banco extranjero"
- Se mantuvieron las marcas internacionales: VISA, Amex, Cybersource, Stripe, Wetravel, Travel Compositor/TravelC. `[decisión]`

## Archivos, tablas y objetos relevantes
- Igual que la memoria anterior. Sólo cambia la columna C (`Nombre`).

## Cambios hechos
- 112 nombres modificados en esta ronda. Contra el original, ninguna columna fuera de la C cambió.

## Errores y cómo se resolvieron
- Algunas celdas comparten el mismo texto interno del xlsx (ej. C37/C38, "Aportes Caja Nacional de Salud"). El script lo permite sólo si todas esas celdas reciben el mismo valor nuevo.

## Riesgos
- Quedan términos tributarios y laborales propios de Bolivia que delatan el origen: IT, IUE, RC IVA, "IVA 13%", "Retencion IT 3%", "Mantenimiento de Valor IVA", "Desahucios", "DPF". No se tocaron: pendiente de decisión de la usuaria.

## Pendientes
- [ ] Decidir si generalizar los términos tributarios y laborales bolivianos.
- [ ] Decidir si corregir los caracteres rotos de la exportación.

## Cómo validar
- En Excel, buscar en la columna C siglas de ciudades o bancos (SRZ, LPB, BCP, BNB, etc.): no deben aparecer.

## Datos que pueden quedar viejos
- Cantidad de cuentas del plan: 586 (foto al 2026-10-08).
