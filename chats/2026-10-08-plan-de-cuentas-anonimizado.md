# Plan de cuentas anonimizado (sin referencias al cliente)

- **Fecha:** 2026-10-08
- **Proyecto / cliente:** Plan de cuentas exportado de un cliente agencia (Tropical / Tropical Tours), para reutilizar sin referencias a él.
- **Actualiza a:** No aplica

## Objetivo
Que ningún nombre de cuenta mencione al cliente Tropical / Estropical / Tropical Tours ni contenga nombres propios. Después se sumó el pedido de quitar los números de cuenta bancaria.

## Estado final
Terminado. Se generó una copia ajustada. El original no se modificó.

## Decisiones y por qué
- No había ninguna mención a Tropical / Estropical / Tropical Tours en ninguna columna. `[datos]`
- Se anonimizaron también otros nombres propios y los números de cuenta bancaria, a pedido de la usuaria. `[decisión]`
- Nombre de agencia → "agencia" (ej. "ARC Transitorio Victory Travel" → "ARC Transitorio agencia"). `[decisión]`
- Sucursales con nombre de shopping, barrio o calle → "Sucursal N" por ciudad, misma numeración para M/E y M/N (SRZ 1–9, LPB 1–2, CBB 1). `[decisión]`
- Bancos: se quitó el número y se dejó banco + moneda + ubicación. Si dos quedaban iguales, se agregó "Cta. 1/2". Tarjetas VISA con últimos 4 dígitos → "Cta. 1/2". `[decisión]`
- Se quitaron las iniciales que podían ser de personas ("HGO" → "Cta. Adicional", "Socio - JV" → "Socio"). `[decisión]`
- Se mantuvieron como genéricos: bancos, procesadores (Cybersource, Stripe, Wetravel), Travel Compositor/TravelC, ECOJET, Abavyt, siglas impositivas. `[decisión]`
- "SANTANDERr" se corrigió a "SANTANDER". `[decisión]`

## Archivos, tablas y objetos relevantes
- Original: `Descargas\PlandeCuentasList_20261008_104108.xlsx` (hoja `Page1`, 586 cuentas, 21 columnas).
- Resultado: `Descargas\PlandeCuentasList_20261008_104108_ajustado.xlsx`.
- Sólo se modificó la columna C (`Nombre`). Códigos (`Nro_cuenta`, `Cuentabcra`), Ids y demás columnas quedaron intactos.

## Cambios hechos
- 68 nombres de cuenta modificados (filas 26–65, 78, 91–136, 145–146, 235, 240–243, 309–310, 401, 480, 485–486, 530–531, 557–560, 582–583).

## Errores y cómo se resolvieron
- No había Python instalado: se editó el .xlsx desde PowerShell, modificando el XML interno (`sharedStrings.xml`).
- Primer intento con textos cruzados: en PowerShell, un diccionario ordenado con claves numéricas `$map[42]` se indexa por posición. Se corrigió iterando con `GetEnumerator()` y se regeneró desde el original.
- Lección: verificar siempre el resultado abriéndolo en Excel y comparando celda por celda contra lo esperado, no sólo contando diferencias.

## Riesgos
- Si el plan se reimporta al sistema, los nombres nuevos pueden no coincidir con lo que espera el cliente. Usarlo sólo como plantilla o demostración.
- Varios nombres originales ya venían con caracteres rotos desde la exportación (ej. "Inflaci�n", "Gesti�n", "A�reo"). No se corrigieron.

## Pendientes
- [ ] Decidir si corregir los caracteres rotos de la exportación.

## Cómo validar
- Abrir el ajustado en Excel y buscar dígitos largos o los nombres reemplazados en la columna C: no deben aparecer.
- Comparar contra el original: sólo deben diferir 68 celdas de la columna C.

## Datos que pueden quedar viejos
- Cantidad de cuentas del plan: 586 (foto al 2026-10-08).
