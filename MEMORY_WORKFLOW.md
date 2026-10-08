# Flujo de memoria

Reglas para crear y mantener las memorias de este repo.

## 1. Una tarea terminada = un archivo nuevo

- Cada tarea terminada produce **un** archivo nuevo en `chats/`.
- Nombre: `AAAA-MM-DD-tema-descriptivo.md` (fecha de cierre de la tarea, tema en minúsculas con guiones, sin tildes ni espacios).
  - Ejemplo: `2026-10-08-relevamiento-agencia-x-modulo-reservas.md`
- Si en el mismo día hay dos tareas del mismo tema, agregar un sufijo: `...-parte-2.md`.

## 2. Los archivos de `chats/` son evidencia histórica

- **No se editan ni se borran.**
- Si algo cambió, se escribe una **memoria nueva** que lo actualiza y referencia a la anterior (link relativo).
- La única excepción es eliminar un dato prohibido (ver `README.md`) subido por error.

## 3. Contenido obligatorio de cada memoria

Usar esta plantilla. Si una sección no aplica, escribir "No aplica".

```markdown
# <Tema>

- **Fecha:** AAAA-MM-DD
- **Proyecto / cliente:** ...
- **Actualiza a:** (link a memoria anterior, si corresponde)

## Objetivo
Qué se buscaba lograr.

## Estado final
Terminado / parcial / bloqueado, y en qué quedó.

## Decisiones y por qué
- Decisión — motivo. [etiqueta]

## Archivos, tablas y objetos relevantes
Documentos, planillas, módulos, tablas, endpoints, contactos por rol (sin datos personales).

## Cambios hechos
Qué se creó o modificó.

## Errores y cómo se resolvieron
- Error — causa — solución.

## Riesgos
Qué puede salir mal o afectar a otros.

## Pendientes
- [ ] Tarea — responsable — fecha si la hay.

## Cómo validar
Pasos concretos para comprobar que lo hecho está bien.

## Datos que pueden quedar viejos
Conteos, IDs, estados, precios, versiones: son "fotos" tomadas en la fecha de esta memoria.
- Dato — valor — (foto al AAAA-MM-DD)
```

## 4. Qué NO incluir

- Razonamiento interno de la IA.
- Transcripción del chat.
- Contraseñas, tokens, cadenas de conexión ni datos personales (ver `README.md`).

## 5. Etiquetas de certeza

Toda afirmación relevante se marca con una de estas etiquetas:

| Etiqueta | Significa |
|---|---|
| `[código]` | Confirmado leyendo código o configuración. |
| `[datos]` | Confirmado consultando datos reales (base, sistema, reporte). |
| `[decisión]` | Decisión funcional o comercial tomada por el usuario/cliente. |
| `[hipótesis]` | Supuesto no verificado o pendiente de confirmar. |

## 6. Consolidación en `PROJECT_MEMORY.md`

Después de crear la memoria:

1. Si aporta conocimiento **transversal y vigente** (regla, decisión, arquitectura, pendiente abierto), reflejarlo en `PROJECT_MEMORY.md`.
2. Agregar la fila al índice de memorias.
3. Lo que quedó obsoleto se **marca como histórico** (ej. `~~texto~~ (histórico desde AAAA-MM-DD, ver chats/...)`), no se borra.
4. Actualizar "Última consolidación".
5. Commit + push.
