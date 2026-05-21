---
name: lotokens
description: Menu para ahorrar tokens — bloquea escritura de .md, desactiva emojis, activa respuestas cortas. Cada funcion es independiente y activable por separado.
user-invocable: true
---

Cuando el usuario invoca esta skill, usa AskUserQuestion con multiSelect: true para mostrar el menu de funciones.

## Menu principal

Pregunta: "LoTokens — selecciona las funciones que deseas activar:"

Opciones disponibles (el usuario puede elegir varias, una, o ninguna):

- **Bloquear .md** — Impide crear o editar cualquier archivo `.md` durante esta sesion.
- **Sin emojis** — Prohibe emojis en todas tus respuestas y en el codigo que generes.
- **Respuesta corta** — Al terminar cualquier tarea responde unicamente: `Listo terminado`

---

## Reglas por funcion

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

Despues de que el usuario seleccione, confirma en una sola linea:

Ejemplo con funciones activas:
`LoTokens activo — Sin emojis | Respuesta corta`

Ejemplo sin ninguna seleccion:
`LoTokens: ninguna funcion activa.`

Aplica las reglas seleccionadas por el resto de la conversacion sin volver a mencionarlas.
