# Manual de Servicio online con marca Softur y sin datos de cliente

- **Fecha:** 2026-11-02
- **Proyecto / cliente:** Softur — material técnico genérico (webservices de cobro online)
- **Actualiza a:** No aplica

## Objetivo
Rearmar el PDF "Manual servicio online" con la marca Softur, sin ningún nombre propio de cliente, usando "Softur" como nombre genérico.

## Estado final
Terminado. PDF de 13 páginas y .docx editable en `Entregables`. Falta que la usuaria confirme la dirección de referencia si el manual se va a usar con una dirección real.

## Decisiones y por qué
- Reemplazos: la URL del cliente (IP y nombre de instancia) pasa a `https://servidor/iTraffic_Softur.ServicePay/ServicePay.svc`, que no es una dirección real; el nombre de la red de cobranza en Usuario, Clave y Origen pasa a Softur / SOFTUR; persona, domicilio y documento de los ejemplos pasan a SOFTUR, "Domicilio de ejemplo" y `12345678`. `[decisión]`
- El elemento `ConsultaRedpagosResponse` del ejemplo de error se unificó como `ConsultaResponse`, igual que el ejemplo de respuesta correcta. `[decisión]`
- `FacturaDGI` se mantuvo: es el nombre real del campo (`Redpagos_consulta.sql`) y DGI no es un cliente. También quedaron Cédula de identidad y Rut como tipos de documento. Delatan el país: confirmar si molesta. `[código]` `[hipótesis]`
- Correcciones menores del original: "En este documento se detalla", numeración 1 a 4 de los servicios (había dos "3."), espacios dentro de etiquetas XML. `[decisión]`
- Se reemplazó el logo gris y naranja del original por el logo Softur vigente; portada e índice quedaron en una sola página. `[decisión]`
- Los ejemplos XML y nombres de parámetro van en Consolas para conservar la alineación; es una excepción a "todo en DM Sans" del manual de marca. `[decisión]`

## Archivos, tablas y objetos relevantes
- Origen: `Downloads/Manual servicio online (2).pdf`.
- Resultado: `Entregables/Manual servicio online (marca Softur).pdf` y `.docx`.
- Softur.Serenity consultado (sólo lectura, con `git pull` previo): `Softur.Serene.Model/Migrations/DefaultDB/ScriptsBD/Sp/Redpagos_consulta.sql` (parámetro `@Origen` declarado y sin otro uso en ese SP; campo `FacturaDGI`). `[código]`
- Plantilla de estilos, tema y logo: `Entregables/Configuracion Facturacion Electronica Uruguay DGI (marca Softur).docx`.

## Cambios hechos
- Se crearon los dos entregables. No se modificó el PDF original ni el repo Softur.Serenity.

## Errores y cómo se resolvieron
- Word no abría el .docx generado — atributos XML cortados por comillas anidadas en PowerShell y orden incorrecto en `pPr` — se usaron comillas simples en los atributos, se corrigió el orden (`keepNext` antes de `pageBreakBefore`) y se agregó un chequeo con `[xml]` antes de empaquetar.
- Bloques XML cortados entre páginas — se agregó `keepNext` a los bloques de hasta 40 líneas.

## Riesgos
- El servicio real puede validar `Origen` o esperar otros nombres de elementos: el manual es de referencia y los valores son ejemplos. Sólo se revisó el SP de consulta, no el código del servicio. `[hipótesis]`
- El .docx conserva en sus propiedades a la usuaria como última persona que lo modificó (no es un cliente).

## Pendientes
- [ ] Confirmar la dirección de referencia y si `FacturaDGI`, Cédula y Rut quedan — usuaria.

## Cómo validar
1. Buscar en el PDF "Tropical", "Redpagos" y el nombre del ejemplo original: no debe haber resultados.
2. Revisar que el índice coincida con las páginas (2, 2, 3, 7, 9, 11, 13).

## Datos que pueden quedar viejos
- Cantidad de páginas — 13 — (foto al 2026-11-02)
