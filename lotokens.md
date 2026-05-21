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
- **Respuesta corta** — Al terminar cualquier tarea responde unicamente: `Listo terminado`

---

## Paso 2 — Persistencia

Si el usuario selecciono al menos una funcion, usa AskUserQuestion (single select) para preguntar:

Pregunta: "Guardar estas preferencias para futuras sesiones?"

Opciones:
- **Solo esta sesion** — Las reglas aplican ahora pero no se guardan.
- **Guardar globalmente** — Escribe las reglas en `~/.claude/CLAUDE.md` (aplica en todos los proyectos).
- **Guardar para este proyecto** — Escribe las reglas en `.claude/CLAUDE.md` (solo este proyecto).

### Si elige guardar (global o proyecto):

Determina la ruta del archivo CLAUDE.md segun la opcion:
- Global: `~/.claude/CLAUDE.md`
- Proyecto: `.claude/CLAUDE.md` (relativo al directorio de trabajo actual)

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
- Incluye README.md, CLAUDE.md, y cualquier otro Markdown
- Si se intenta, responde exactamente: `Bloqueado por LoTokens: escritura de .md desactivada.`
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
- Al completar cualquier tarea escribe unicamente: `Listo terminado`
- Sin resumen, sin contexto, sin explicacion de lo realizado
- Si el usuario hace una pregunta directa (no una tarea), responde solo lo minimo necesario
```

Si el usuario elige "Solo esta sesion", omite este paso por completo.

---

## Reglas por funcion (para esta sesion)

### Bloquear .md
- NO uses Write ni Edit sobre archivos con extension `.md`
- Incluye README.md, CLAUDE.md, y cualquier otro Markdown
- Si se intenta, responde exactamente: `Bloqueado por LoTokens: escritura de .md desactivada.`

### Sin emojis
- NO incluyas emojis en respuestas de texto
- NO incluyas emojis en comentarios de codigo, strings ni documentacion inline
- Aplica durante toda la sesion

### Respuesta corta
- Al completar cualquier tarea escribe unicamente: `Listo terminado`
- Sin resumen, sin contexto, sin explicacion de lo realizado
- Si el usuario hace una pregunta directa (no una tarea), responde solo lo minimo necesario

---

## Confirmacion al usuario

Despues de completar ambos pasos, confirma en una o dos lineas:

Ejemplo con funciones activas y guardado global:
`LoTokens activo — Sin emojis | Respuesta corta`
`Preferencias guardadas en ~/.claude/CLAUDE.md`

Ejemplo solo esta sesion:
`LoTokens activo — Bloquear .md | Sin emojis`

Ejemplo sin ninguna seleccion:
`LoTokens: ninguna funcion activa.`

Aplica las reglas seleccionadas por el resto de la conversacion sin volver a mencionarlas.
