# Proceso por sector v2 — Cuenca del Plata: pedidos de carga por correo al equipo de tarifas

- **Fecha:** 2026-10-30
- **Proyecto / cliente:** Softur — implementación iTraffic, cliente Cuenca del Plata
- **Actualiza a:** [2026-10-30-proceso-por-sector-v2-cuenca-del-plata-emisivo.md](2026-10-30-proceso-por-sector-v2-cuenca-del-plata-emisivo.md)

## Objetivo
Dejar explícito que los pedidos de carga se formalizan por correo al equipo de tarifas.

## Estado final
Terminado. `Trabajo/Entregables/Proceso por sector v2 - Cuenca del Plata (marca Softur).docx` (+ `.pdf`, 13 páginas).

## Decisiones y por qué
- Regla: todo pedido de carga (productos y tarifas) se formaliza **por correo al equipo de tarifas**. `[decisión]`
- Portada: la regla se sumó a la celda "Regla de oro" (una fila nueva empujaba "Cómo leer cada página" a una segunda hoja). `[decisión]`
- Se cambiaron los pedidos de palabra: Reservas paso 2 (producto muy vendido inexistente) y paso 7 (ítem de guía inexistente), Costeo/Facundo paso 3 (sin tarifa de costo): "se pide a Producto / Cargas" → "se pide por correo al equipo de tarifas"; Hoteles/Luz paso 2: "Pide a Ventas, o por correo al equipo de tarifas, que corrijan la tarifa". Los "Recurrir a Producto / Cargas" no se tocaron. `[decisión]`

## Archivos, tablas y objetos relevantes
- Script `pedidos-carga.ps1` (scratchpad). Softur.Serenity: no se consultó.

## Cambios hechos
- Word y PDF reemplazados en Entregables.

## Errores y cómo se resolvieron
- En PowerShell las variables no distinguen mayúsculas: un `foreach ($e ...)` pisó `$E` (carpeta de destino) y la copia falló sin escribir nada — usar nombres distintos (`$ext`, `$Dest`).

## Riesgos
No aplica.

## Pendientes
No aplica.

## Cómo validar
1. PDF página 1: "Regla de oro" incluye el correo al equipo de tarifas; página 2, globo del paso 2 de Reservas.

## Datos que pueden quedar viejos
No aplica.
