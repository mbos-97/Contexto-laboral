# Carga de un ticket aéreo de cabotaje en la tarifa de un eventual

- **Fecha:** 2026-10-30
- **Proyecto / cliente:** Softur — consulta funcional general (iTraffic / Serenity), sin cliente puntual

## Objetivo
Explicar campo por campo de la tarifa de un eventual dónde se carga un ticket aéreo de cabotaje (tarifa, IVA, tasas, comisión, fee).

## Estado final
Respondido en el chat (sin documento).

## Hallazgos
- Pantalla Eventual: secciones Datos Generales (Tipo `Ts` → ParameTable `PRES`, obligatorio; Tipo contratación `Comodin` → `CGAR`; Centro Costo → `CECO`), Información (Descripción, Descripción Detallada), Prestador y Operador (Proveedor, Operador), Destino y Período (Destino obligatorio, Desde, Hasta, Cant. Días, Noches), Precio (Categoría, Prioridad → `TPRI`, Moneda Local, Moneda Vta., Cambio) y "Tarifas según Base". `[código]`
- Cada fila de "Tarifas según Base" (tabla `Eventuah`) es una combinación Habitación + Tipo Pax, con: Costo (`Costiphab`), Precio (`Pretiphab`), Comisión, Over (campo `Descuento`), Impuesto, Tasa, Fee (oculto), Costo Total, Precio Total, No Gravado, y Plantilla / Utilidad (default 1) / Comisión (%). Los rótulos salen de traducciones y pueden variar por cliente. `[código]`
- Dentro de cada fila, la grilla de conceptos (tabla `Eventuac`): Concepto, Tasa, Base Costo, Impuesto Costo, Base Venta, Impuesto Venta. El impuesto de cada concepto se calcula solo: base × tasa / 100. Al editar, Costo Total = Σ(base + impuesto costo) y Precio Total = Σ(base + impuesto venta). `[código]`
- Conceptos de fábrica (tabla `Concepto`): 1 GRAVADO, 2 NO GRAVADO, 3 EXENTO ("EXENTOS TRANSPORTES"), **4 GRAV_AEREO = "GRAVADO TRANSPORTE CABOTAJE"**, 5 OTROGRAVADO ("PERCEPCIONES"). La tasa viene en 0 en el seed: cada base la configura. `[código]`
- Las plantillas de precios con lógica `DIFF` asumen que Σ bases de conceptos = Precio (o Costo) + Tasa + Impuesto; o sea que el IVA no se carga en Impuesto, lo calculan los conceptos. `[código]`
- Criterio propuesto para cabotaje: tarifa → base del concepto GRAV_AEREO (con su tasa, normalmente 10,5%); tasas aeroportuarias → campo Tasa y concepto NO GRAVADO (o EXENTO, según el contador); fee/utilidad de la agencia → GRAVADO (21%); percepciones → PERCEPCIONES. `[hipótesis]` (validar con la configuración contable de cada agencia)

## Archivos, tablas y objetos relevantes
- Softur.Serenity (sólo lectura):
  - `Softur.Serene.Web/Modules/B_Tarifas/Eventual/EventualForm.generated.cs`
  - `Softur.Serene.Web/Modules/B_Tarifas/Eventuah/EventuahForm.generated.cs`, `EventuahEditorDialog.ts` (recálculo, plantillas, DIFF)
  - `Softur.Serene.Web/Modules/B_Tarifas/Eventuac/EventuacColumns.generated.cs`, `EventuacEditor.ts`
  - `Softur.Serene.Model/Migrations/DefaultDB/Scripts/20171002_160200_Datos_Iniciales.sql` (seed de `Concepto`)
  - Tablas: `Eventual`, `Eventuah`, `Eventuac`, `Concepto`, `PlantillaPrecios`, `PlantillaPreciosDet`

## Pendientes
- [ ] Confirmar en la base del cliente la tasa de GRAV_AEREO y si las tasas aeroportuarias van a NO GRAVADO o EXENTO — usuaria/cliente.
