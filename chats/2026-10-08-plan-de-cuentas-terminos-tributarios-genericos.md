# Plan de cuentas: términos tributarios y laborales genéricos

- **Fecha:** 2026-10-08
- **Proyecto / cliente:** Plan de cuentas de cliente agencia, para usar como plantilla genérica.
- **Actualiza a:** [2026-10-08-plan-de-cuentas-sin-ciudades-ni-bancos.md](2026-10-08-plan-de-cuentas-sin-ciudades-ni-bancos.md) (resuelve su primer pendiente)

## Objetivo
Generalizar los términos tributarios y laborales propios de Bolivia para que el plan no delate el país.

## Estado final
Terminado sobre `Descargas\PlandeCuentasList_20261008_104108_ajustado.xlsx`. En total, contra el original cambiaron 131 nombres y ninguna otra columna.

## Decisiones y por qué
- Criterios de reemplazo: `[decisión]`
  - IT → "Impuesto a las Transacciones"
  - IUE / "Utilidades de las Empresas" → "Impuesto a las Ganancias" ("Imp. Ganancias" en las retenciones, por el límite de 50 caracteres)
  - RC IVA → "Retencion Imp. Renta"
  - "IVA 13%" → "IVA"; "Retencion IT 3%" → sin porcentaje
  - A.I.T.B. y "Ajuste por Inflación y Tenencia de Bienes" → "Ajuste por Inflacion"
  - "Mantenimiento de Valor IVA" → "Actualizacion Monetaria IVA"
  - "Desahucios" → "Indemnizacion por Preaviso"
  - "Valores DPF" → "Plazo Fijo"
- Se mantuvieron por ser genéricos: Crédito/Débito Fiscal IVA, "Impuesto a las Transacciones Financieras", Aguinaldos, Bonos de Antigüedad, Subsidios, "Compensacion Tributaria". `[decisión]`

## Archivos, tablas y objetos relevantes
- Igual que las memorias anteriores. Sólo cambia la columna C (`Nombre`).

## Cambios hechos
- 17 nombres modificados en esta ronda: C2, C17, C31, C209, C320, C322, C396–398, C400, C408, C511–512, C525–528.

## Errores y cómo se resolvieron
- No aplica.

## Riesgos
- Algunos nombres siguen teniendo caracteres rotos de la exportación (ej. "Penalidades Internacional A�reo", "Resultados de la Gesti�n"). El de C17 quedó corregido de paso.

## Pendientes
- [ ] Decidir si corregir los caracteres rotos restantes.

## Cómo validar
- En Excel, buscar en la columna C "IT", "IUE", "RC IVA", "13%", "DPF": no deben aparecer como siglas.

## Datos que pueden quedar viejos
- Cantidad de cuentas del plan: 586 (foto al 2026-10-08).
