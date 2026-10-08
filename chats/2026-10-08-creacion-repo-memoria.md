# Creación del repo de memoria

- **Fecha:** 2026-10-08
- **Proyecto / cliente:** Contexto-Laboral (uso interno)
- **Actualiza a:** No aplica (primera memoria)

## Objetivo
Crear un repositorio de memoria persistente que la IA lea al empezar cada tarea y alimente al terminarla, para el trabajo diario como comercial en Softur.

## Estado final
Terminado. Estructura base creada y subida a `main`. Quedan pendientes los datos del proyecto principal.

## Decisiones y por qué
- Memorias por tarea en `chats/`, inmutables — conservar evidencia histórica y evitar perder contexto al reescribir. `[decisión]`
- `PROJECT_MEMORY.md` como síntesis con orden de prioridad explícito — resolver contradicciones entre memoria vieja y realidad actual. `[decisión]`
- Etiquetas de certeza (`[código]`, `[datos]`, `[decisión]`, `[hipótesis]`) — distinguir lo verificado de lo supuesto. `[decisión]`
- Clon local en `C:\Users\mbos\OneDrive\Desktop\Trabajo\Contexto-laboral`. `[decisión]`

## Archivos, tablas y objetos relevantes
- `README.md`, `MEMORY_WORKFLOW.md`, `PROJECT_MEMORY.md`, `chats/`.
- Remoto: https://github.com/mbos-97/Contexto-laboral

## Cambios hechos
- Instalado Git para Windows (2.55.0) vía winget en la PC de trabajo.
- Creados los 4 elementos de la estructura y primer commit + push.

## Errores y cómo se resolvieron
- Git no estaba instalado — se instaló con `winget install Git.Git`.
- Git sin identidad configurada — se configuró nombre y mail sólo a nivel de este repo.

## Riesgos
- Que se suban datos sensibles por descuido (clientes, pasajeros, credenciales). Mitigación: regla explícita en `README.md`.

## Pendientes
- [ ] Definir proyecto principal, stack y repos de código involucrados — usuaria.
- [ ] Registrar reglas laborales ya conocidas — usuaria.

## Cómo validar
- Abrir https://github.com/mbos-97/Contexto-laboral y verificar que están los 3 `.md` y `chats/` con esta memoria.

## Datos que pueden quedar viejos
- Versión de Git instalada — 2.55.0 — (foto al 2026-10-08)
