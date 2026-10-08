# Contexto-Laboral

Repositorio de **memoria persistente** para el trabajo diario en Softur (venta de software para agencias de turismo): relevamientos, pedidos técnicos, propuestas comerciales y proyectos.

La IA que asiste en las tareas **lee** esta memoria al empezar cada tarea y la **alimenta** al terminarla.

## Estructura

| Ruta | Qué contiene |
|---|---|
| `README.md` | Este archivo: qué es el repo y cómo se usa. |
| `MEMORY_WORKFLOW.md` | Reglas para escribir y mantener las memorias. |
| `PROJECT_MEMORY.md` | Memoria consolidada: conocimiento transversal y vigente + índice. |
| `chats/` | Una memoria por tarea terminada (`AAAA-MM-DD-tema-descriptivo.md`). Histórico inmutable. |

## Cómo se usa

**Al empezar una tarea**
1. Leer `PROJECT_MEMORY.md` completo.
2. Desde su índice, abrir las memorias de `chats/` relacionadas con el tema.
3. Ante contradicciones, aplicar el orden de prioridad definido en `PROJECT_MEMORY.md`.

**Al terminar una tarea**
1. Crear **un** archivo nuevo en `chats/` siguiendo `MEMORY_WORKFLOW.md`.
2. Si cambió algo transversal (regla, decisión, pendiente), actualizar `PROJECT_MEMORY.md` y su índice.
3. Commit + push.

## ⚠️ Prohibido guardar en este repo

Este repo **NUNCA** debe contener:

- Contraseñas, PINs o claves de cualquier tipo.
- Tokens, API keys, secretos de OAuth o certificados.
- Cadenas de conexión (a bases de datos, servicios, VPNs, etc.).
- Datos personales: DNI/CUIT de personas, teléfonos o mails personales, domicilios, datos de pasajeros, datos de tarjetas o bancarios.

Si hace falta referirse a uno de esos datos, se describe **dónde** está (ej. "credencial guardada en el gestor de contraseñas de la empresa") sin copiar el valor. Si algo de esto se sube por error, no alcanza con borrarlo en un commit nuevo: queda en el historial y hay que rotar el secreto y limpiar el historial.
