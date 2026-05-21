---
name: lotokens
description: Menu para ahorrar tokens — bloquea escritura de .md, desactiva emojis, activa respuestas cortas. Cada funcion es independiente y activable por separado. Permite guardar preferencias de forma persistente en CLAUDE.md.
user-invocable: true
---

Cuando el usuario invoca esta skill, sigue estos pasos en orden:

## Paso 1 — Menu principal

Usa AskUserQuestion con multiSelect: true.

Pregunta: "LoTokens — selecciona las funciones que deseas activar:"

Opciones disponibles (el usuario puede elegir varias, una, o ninguna):

- **Bloquear .md** — Impide crear o editar cualquier archivo `.md` durante esta sesion.
- **Sin emojis** — Prohibe emojis en todas tus respuestas y en el codigo que generes.
- **Respuesta corta** — Al completar cualquier tarea (cuando usas herramientas), responde unicamente: `Listo`

---

## Paso 2 — Persistencia

Si el usuario selecciono al menos una funcion, usa AskUserQuestion (single select) para preguntar:

Pregunta: "Guardar estas preferencias para futuras sesiones?"

Opciones:
- **Solo esta sesion** — Las reglas aplican a TODA la sesion hasta que termines. No se guarda nada en disco.
- **Guardar globalmente** — Escribe las reglas en el CLAUDE.md global (aplica en todos los proyectos).
- **Guardar para este proyecto** — Escribe las reglas en `.claude/CLAUDE.md` (solo este proyecto).

### Rutas segun sistema operativo

Detecta el sistema operativo antes de escribir:

- Linux / macOS — Global: `~/.claude/CLAUDE.md` | Proyecto: `.claude/CLAUDE.md`
- Windows — Global: `%USERPROFILE%\.claude\CLAUDE.md` | Proyecto: `.claude\CLAUDE.md`

Para detectar Windows: verifica si la variable de entorno `USERPROFILE` existe o si el path separator es `\`. Si no puedes detectarlo, usa `~/.claude/CLAUDE.md` como fallback y advierte al usuario que en Windows debe usar `%USERPROFILE%\.claude\CLAUDE.md`.

### Si elige guardar (global o proyecto):

Lee el archivo CLAUDE.md si existe. Luego agrega (o reemplaza si ya existe una seccion `## LoTokens`) el siguiente bloque con solo las reglas de las funciones seleccionadas:

```
## LoTokens

<!-- Generado automaticamente por la skill LoTokens. Edita o elimina esta seccion para cambiar las preferencias. -->

[incluye solo las reglas de las funciones que el usuario selecciono]
```

Reglas por funcion para escribir en CLAUDE.md:

**Bloquear .md:**
```
### Bloquear .md
- NO uses Write ni Edit sobre archivos con extension `.md`
- Incluye README.md y cualquier otro Markdown
- EXCEPCION: puedes editar CLAUDE.md unicamente cuando el usuario invoca /lotokens para guardar preferencias
- Si se intenta escribir otro .md, responde exactamente: `Bloqueado por LoTokens: escritura de .md desactivada.`
```

**Sin emojis:**
```
### Sin emojis
- NO incluyas emojis en respuestas de texto
- NO incluyas emojis en comentarios de codigo, strings ni documentacion inline
```

**Respuesta corta:**
```
### Respuesta corta
- Una "tarea" es cualquier accion que requiera usar herramientas (Write, Edit, Bash, Read, Glob, Grep, etc.)
- Una "pregunta" es cualquier solicitud de informacion o explicacion sin uso de herramientas
- Al completar una TAREA: responde UNICAMENTE la palabra `Listo` — sin resumen, sin lista de cambios, sin contexto
- Al responder una PREGUNTA: responde de forma concisa (maximo 2-3 oraciones), sin detalle excesivo
- Si el usuario pide explicitamente que expliques algo: es una pregunta, responde concisamente
- Esta regla aplica a TODAS las respuestas siguientes en la sesion
```

### Caso especial: "Bloquear .md" + guardar en CLAUDE.md

Si el usuario selecciona "Bloquear .md" y tambien elige guardar (global o proyecto):
- Permite escribir en CLAUDE.md UNA SOLA VEZ como operacion de configuracion inicial
- Despues de guardar, la regla "Bloquear .md" entra en efecto para el resto de la sesion
- Esto es el unico caso donde Write sobre un `.md` esta permitido mientras "Bloquear .md" esta activo

Si el usuario elige "Solo esta sesion", omite escribir archivos por completo.

---

## Reglas por funcion (para esta sesion)

Las siguientes reglas aplican INMEDIATAMENTE desde el momento en que el usuario las selecciona, para toda la sesion hasta que termine.

### Bloquear .md
- NO uses Write ni Edit sobre archivos con extension `.md`
- Incluye README.md y cualquier otro Markdown
- EXCEPCION: puedes editar CLAUDE.md unicamente cuando el usuario invoca /lotokens para guardar preferencias
- Si se intenta, responde exactamente: `Bloqueado por LoTokens: escritura de .md desactivada.`

### Sin emojis
- NO incluyas emojis en respuestas de texto
- NO incluyas emojis en comentarios de codigo, strings ni documentacion inline

### Respuesta corta
- Una "tarea" es cualquier accion que requiera usar herramientas (Write, Edit, Bash, Read, Glob, Grep, etc.)
- Una "pregunta" es cualquier solicitud de informacion o explicacion sin uso de herramientas
- Al completar una TAREA: responde UNICAMENTE la palabra `Listo` — sin resumen, sin lista de cambios, sin contexto
- Al responder una PREGUNTA: responde de forma concisa (maximo 2-3 oraciones), sin detalle excesivo
- Si el usuario pide explicitamente que expliques algo: es una pregunta, responde concisamente
- Esta regla aplica a TODAS las respuestas siguientes en la sesion, incluyendo la confirmacion de LoTokens

---

## Confirmacion al usuario

IMPORTANTE: Si "Respuesta corta" esta activa, aplica esa regla TAMBIEN a esta confirmacion.

Si "Respuesta corta" esta activa — confirmacion en UNA SOLA linea:
`LoTokens activo — [funciones activas separadas por |] — [guardado/solo sesion]`

Si "Respuesta corta" NO esta activa — confirmacion en una o dos lineas:

Ejemplo con funciones activas y guardado global:
`LoTokens activo — Sin emojis | Respuesta corta`
`Preferencias guardadas en ~/.claude/CLAUDE.md`

Ejemplo solo esta sesion:
`LoTokens activo — Bloquear .md | Sin emojis`

Ejemplo sin ninguna seleccion:
`LoTokens: ninguna funcion activa.`

Aplica las reglas seleccionadas por el resto de la conversacion sin volver a mencionarlas.
