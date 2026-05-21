# Skill-LoTokens

A Claude Code skill to reduce token usage during your sessions. Activate only what you need from an interactive menu. Optionally save your preferences to persist them across sessions.

---

## Functions

| Function | What it does |
|---|---|
| **Block .md** | Prevents Claude from creating or editing any `.md` file in your project |
| **No emojis** | Removes emojis from all responses and generated code |
| **Short response** | After completing any task, Claude replies only: `Listo terminado` |

Each function is independent — activate one, two, or all three.

---

## Installation

**Option 1 — Global (available in all projects):**

macOS / Linux:
```bash
curl -o ~/.claude/skills/lotokens.md \
  https://raw.githubusercontent.com/AngyLabs/Skill-LoTokens/main/lotokens.md
```

Windows (PowerShell):
```powershell
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/AngyLabs/Skill-LoTokens/main/lotokens.md" `
  -OutFile "$env:USERPROFILE\.claude\skills\lotokens.md"
```

**Option 2 — Manual:**

Download `lotokens.md` and copy it to:

macOS / Linux:
- `~/.claude/skills/` — global install
- `.claude/skills/` — local to a specific project

Windows:
- `%USERPROFILE%\.claude\skills\` — global install
- `.claude\skills\` — local to a specific project

---

## Usage

In any Claude Code session, type:

```
/lotokens
```

An interactive menu will appear. Select the functions you want to activate.

After selecting, Claude will ask where to save your preferences:

| Option | Behavior |
|---|---|
| **This session only** | Rules apply now, nothing is saved to disk |
| **Save globally** | Rules are written to `~/.claude/CLAUDE.md` and apply in all projects |
| **Save for this project** | Rules are written to `.claude/CLAUDE.md` and apply only here |

When saved, Claude writes a `## LoTokens` block to the target `CLAUDE.md`. On future sessions, the rules are active automatically — no need to run `/lotokens` again.

To update or remove saved preferences, run `/lotokens` again or manually edit the `## LoTokens` section in the corresponding `CLAUDE.md`.

---

## Example

```
/lotokens

LoTokens — select the functions you want to activate:
  [x] No emojis
  [x] Short response
  [ ] Block .md

Save these preferences for future sessions?
  > Save globally (~/.claude/CLAUDE.md)

LoTokens active — No emojis | Short response
Preferences saved in ~/.claude/CLAUDE.md
```

---

## Compatibility

- Claude Code CLI
- Claude Code desktop app
- Claude Code IDE extensions (VS Code, JetBrains)
- Windows, macOS, Linux

---

Built for [Claude Code](https://claude.ai/code) by AngyLabs.

---
---

# Skill-LoTokens — Documentacion en Español

Una skill para Claude Code que reduce el uso de tokens en tus sesiones. Activa solo lo que necesitas desde un menu interactivo. Guarda tus preferencias para que persistan entre sesiones.

---

## Funciones

| Funcion | Que hace |
|---|---|
| **Bloquear .md** | Impide que Claude cree o edite cualquier archivo `.md` en tu proyecto |
| **Sin emojis** | Elimina emojis de todas las respuestas y del codigo generado |
| **Respuesta corta** | Al terminar cualquier tarea, Claude responde unicamente: `Listo terminado` |

Cada funcion es independiente: activa una, dos, o las tres.

---

## Instalacion

**Opcion 1 — Global (disponible en todos los proyectos):**

macOS / Linux:
```bash
curl -o ~/.claude/skills/lotokens.md \
  https://raw.githubusercontent.com/AngyLabs/Skill-LoTokens/main/lotokens.md
```

Windows (PowerShell):
```powershell
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/AngyLabs/Skill-LoTokens/main/lotokens.md" `
  -OutFile "$env:USERPROFILE\.claude\skills\lotokens.md"
```

**Opcion 2 — Manual:**

Descarga `lotokens.md` y copialo a:

macOS / Linux:
- `~/.claude/skills/` — instalacion global
- `.claude/skills/` — solo para este proyecto

Windows:
- `%USERPROFILE%\.claude\skills\` — instalacion global
- `.claude\skills\` — solo para este proyecto

---

## Uso

En cualquier sesion de Claude Code, escribe:

```
/lotokens
```

Aparecera un menu interactivo. Selecciona las funciones que deseas activar.

Despues de seleccionar, Claude preguntara donde guardar tus preferencias:

| Opcion | Comportamiento |
|---|---|
| **Solo esta sesion** | Las reglas aplican ahora, no se guarda nada en disco |
| **Guardar globalmente** | Las reglas se escriben en `~/.claude/CLAUDE.md` y aplican en todos los proyectos |
| **Guardar para este proyecto** | Las reglas se escriben en `.claude/CLAUDE.md` y aplican solo aqui |

Al guardar, Claude escribe un bloque `## LoTokens` en el `CLAUDE.md` correspondiente. En futuras sesiones las reglas estaran activas automaticamente — no necesitas volver a ejecutar `/lotokens`.

Para actualizar o eliminar las preferencias guardadas, vuelve a ejecutar `/lotokens` o edita manualmente la seccion `## LoTokens` en el `CLAUDE.md` correspondiente.

---

## Ejemplo

```
/lotokens

LoTokens — selecciona las funciones que deseas activar:
  [x] Sin emojis
  [x] Respuesta corta
  [ ] Bloquear .md

Guardar estas preferencias para futuras sesiones?
  > Guardar globalmente (~/.claude/CLAUDE.md)

LoTokens activo — Sin emojis | Respuesta corta
Preferencias guardadas en ~/.claude/CLAUDE.md
```

---

## Compatibilidad

- Claude Code CLI
- Claude Code app de escritorio
- Extensiones IDE de Claude Code (VS Code, JetBrains)
- Windows, macOS, Linux

---

Desarrollado para [Claude Code](https://claude.ai/code) por AngyLabs.
