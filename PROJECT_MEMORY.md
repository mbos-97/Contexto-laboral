# Memoria del proyecto — Contexto-Laboral

**Última consolidación:** 2026-10-08

## 1. Cómo leer esta memoria

Ante información contradictoria, vale este orden de prioridad (de mayor a menor):

1. **Decisión nueva del usuario** en la tarea actual.
2. **Código / datos actuales verificados.**
3. **Memoria más reciente** en `chats/`.
4. **Esta síntesis** (`PROJECT_MEMORY.md`).

Esta síntesis contiene sólo conocimiento transversal y vigente; el detalle está en `chats/`. Las reglas de escritura están en [MEMORY_WORKFLOW.md](MEMORY_WORKFLOW.md).

## 2. Contexto y arquitectura

- **Usuaria:** comercial en Softur. `[decisión]`
- **Empresa:** Softur — venta de software para agencias de turismo. `[decisión]`
- **Uso del repo:** contexto para el trabajo diario: relevamientos con clientes/prospectos, pedidos técnicos, propuestas y seguimiento de proyectos. `[decisión]`
- **Proyecto principal:** _pendiente — la usuaria lo va a compartir más adelante._ `[hipótesis]`
- **Stack / productos involucrados:** _pendiente._
- **Repos de código involucrados:** _pendiente._ Por ahora sólo este repo:
  - Contexto-Laboral — https://github.com/mbos-97/Contexto-laboral

## 3. Reglas y decisiones vigentes

- Nunca guardar contraseñas, tokens, cadenas de conexión ni datos personales (incluye datos de pasajeros y de clientes personas físicas). `[decisión]`
- Cada tarea terminada genera una memoria nueva en `chats/`; las memorias no se editan ni se borran. `[decisión]`
- Toda afirmación relevante lleva etiqueta de certeza: `[código]`, `[datos]`, `[decisión]`, `[hipótesis]`. `[decisión]`
- Material de un cliente que se reutiliza (ej. planes de cuentas) se anonimiza y se vuelve genérico: nada del nombre del cliente, nombres propios, sucursales, ciudades, bancos, números de cuenta o tarjeta, ni entidades que delaten el país. Reemplazos: cliente o agencia → "agencia", sucursal → "Sucursal N", ciudad → "Ciudad N", banco → "Banco N". Las siglas tributarias locales se escriben con su nombre genérico (ej. IUE → "Impuesto a las Ganancias", sin alícuotas como "13%"); ver [chats/2026-10-08-plan-de-cuentas-terminos-tributarios-genericos.md](chats/2026-10-08-plan-de-cuentas-terminos-tributarios-genericos.md). Ver [chats/2026-10-08-plan-de-cuentas-sin-ciudades-ni-bancos.md](chats/2026-10-08-plan-de-cuentas-sin-ciudades-ni-bancos.md). `[decisión]`
- Entorno de la PC: no hay Python. Excel sí está instalado (se puede usar por COM desde PowerShell para validar). Git está en `C:\Program Files\Git\cmd` (agregarlo al PATH vía `$env:ProgramFiles`). `[datos]`
- Otras reglas de trabajo propias de Softur o de clientes: _pendiente de relevar con la usuaria._

## 4. Pendientes

- [ ] Completar proyecto principal, stack y repos de código involucrados.
- [ ] Registrar reglas laborales ya conocidas (formatos de propuesta, circuito de pedidos técnicos, aprobaciones, etc.).

## 5. Índice de memorias

| Tema | Memoria |
|---|---|
| Creación del repo de memoria | [chats/2026-10-08-creacion-repo-memoria.md](chats/2026-10-08-creacion-repo-memoria.md) |
| Plan de cuentas anonimizado (sin referencias al cliente Tropical) | [chats/2026-10-08-plan-de-cuentas-anonimizado.md](chats/2026-10-08-plan-de-cuentas-anonimizado.md) |
| Plan de cuentas genérico (sin ciudades, bancos ni referencias a Bolivia) | [chats/2026-10-08-plan-de-cuentas-sin-ciudades-ni-bancos.md](chats/2026-10-08-plan-de-cuentas-sin-ciudades-ni-bancos.md) |
| Plan de cuentas: términos tributarios y laborales genéricos | [chats/2026-10-08-plan-de-cuentas-terminos-tributarios-genericos.md](chats/2026-10-08-plan-de-cuentas-terminos-tributarios-genericos.md) |
