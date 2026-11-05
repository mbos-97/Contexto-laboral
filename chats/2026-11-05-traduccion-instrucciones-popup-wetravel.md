# Traducción de las instrucciones para abrir WeTravel en un popup

- **Fecha:** 2026-11-05
- **Proyecto / cliente:** No identificado
- **Actualiza a:** No aplica

## Objetivo
Traducir al español instrucciones en inglés para abrir el checkout de WeTravel en un popup en lugar de redirigir a otra pestaña.

## Estado final
Terminado. Traducción entregada en el chat; no se implementó nada.

## Decisiones y por qué
- Resumen del método: un botón BNB de WeTravel oculto, sin `href` ni `data-uuid`; al crearse el link, JavaScript completa esos atributos con el UUID de la respuesta de la API y dispara el clic. Conviene no crear un link nuevo en cada clic. [datos]
- "BNB" probablemente significa "Book Now Button"; el texto no lo aclara. [hipótesis]

## Archivos, tablas y objetos relevantes
Softur.Serenity no se consultó: fue sólo una traducción.

## Cambios hechos
Se creó esta memoria.

## Errores y cómo se resolvieron
No aplica

## Riesgos
No se verificó el método contra la documentación de WeTravel ni contra código.

## Pendientes
No aplica

## Cómo validar
No aplica

## Datos que pueden quedar viejos
No aplica
