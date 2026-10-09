# Acceso al TFS y clonado de Softur.Serenity

- **Fecha:** 2026-10-09
- **Proyecto / cliente:** Softur (interno) — repo Softur.Serenity
- **Actualiza a:** No aplica

## Objetivo
Clonar el repo de código del sistema Softur/Serenity desde el TFS de la empresa y dejar establecido que se consulte ese repo en toda tarea sobre procesos de Softur/Serenity.

## Estado final
Terminado. El repo quedó clonado en `C:\Users\mbos\source\repos\Softur.Serenity` y la regla de consultarlo quedó en `..\CLAUDE.md` (carpeta Trabajo) y en `PROJECT_MEMORY.md`. `[datos]`

## Decisiones y por qué
- Toda consulta sobre procesos, módulos, pantallas o tablas de Softur/Serenity se responde leyendo primero ese repo (con `git pull` antes): ahí está todo el sistema. `[decisión]`
- El repo Softur.Serenity es sólo lectura en estas tareas, salvo pedido explícito: evitar cambios accidentales en el código productivo. `[decisión]`
- La regla se puso en `CLAUDE.md` de la carpeta Trabajo para que se cargue sola en cada chat. `[decisión]`

## Archivos, tablas y objetos relevantes
- Remoto: `http://tfs.softur.com.ar:8080/tfs/DefaultCollection/Softur/_git/Softur.Serenity` (TFS on-premise, proyecto "Softur"). `[datos]`
- Soluciones en la raíz: `Softur.Serenity.sln`, `Softur.Serene.Generator.sln`, `Softur.Serenity.Generator.sln`. Carpetas: `Softur.Serene`, `Softur.Data`, `Serenity.Extensions`, `Rate.Engine`, `Plugins`, `Pdf Generator`, `Softur.CodeGenerator`, `Softur.Socios.Aca`, entre otras. `[código]`
- `C:\Users\mbos\OneDrive\Desktop\Trabajo\CLAUDE.md` — instrucciones de arranque de cada chat. `[datos]`

## Cambios hechos
- Se borró la credencial guardada `MELANIE\m.bos` del TFS en el administrador de credenciales.
- Se habilitó NTLM en git sólo para el host del TFS: `git config --global http.http://tfs.softur.com.ar:8080.allowNTLMAuth true`.
- Se creó `CLAUDE.md` en la carpeta Trabajo y se actualizó `PROJECT_MEMORY.md`.

## Errores y cómo se resolvieron
- "Authentication failed" al clonar — el usuario se mandaba sin dominio y Windows le agregaba el nombre de la PC (`MELANIE\`); el TFS usa cuentas locales del servidor — usar `WIN-5B77K21K4NL\<usuario>`. `[datos]`
- Credencial incorrecta cacheada — git la reutilizaba en cada intento — se borró con `git credential-manager erase`.
- "destination path already exists" — quedó un `.git` vacío de un clone fallido — se borró la carpeta y se volvió a clonar.
- Git 2.55 rechaza NTLM por defecto ("NTLM authentication has been disabled") — se habilitó por host (ver arriba). `[datos]`

## Riesgos
- El TFS va por HTTP sin cifrar y NTLM es débil: no reutilizar esa contraseña en otros sistemas.
- Una contraseña quedó expuesta en un chat: se recomendó cambiarla.

## Pendientes
- [ ] Cambiar la contraseña del TFS — usuaria.
- [ ] Revisar si la credencial de `test.ringo.softur.com.ar` (guardada como `MELANIE\m.bos`) también necesita el prefijo `WIN-5B77K21K4NL\` — usuaria.

## Cómo validar
- `git -C C:\Users\mbos\source\repos\Softur.Serenity pull` termina sin pedir credenciales ni dar error.

## Datos que pueden quedar viejos
- Versión de Git — 2.55.0.windows.5 — (foto al 2026-10-09)
- Nombre del servidor TFS — WIN-5B77K21K4NL — (foto al 2026-10-09)
