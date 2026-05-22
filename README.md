# Skill-LoTokens

A Claude Code skill to reduce token usage during your sessions. Activate only what you need from an interactive menu. Optionally save your preferences to persist them across sessions.

---

## Functions

| Function | What it does |
|---|---|
| **Block .md** | Prevents Claude from creating or editing any `.md` file in your project |
| **No emojis** | Removes emojis from all responses and generated code |
| **Short response** | After completing any task (tool use), Claude replies only: `Listo` |

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
| **Save globally** | Rules are written to `~/.claude/CLAUDE.md` (Linux/macOS) or `%USERPROFILE%\.claude\CLAUDE.md` (Windows) and apply in all projects |
| **Save for this project** | Rules are written to `.claude/CLAUDE.md` in the current directory and apply only here |

### How persistent memory works

When you choose to save, Claude writes a `## LoTokens` block into the target `CLAUDE.md` file. Claude Code automatically loads `CLAUDE.md` at the start of every session, so your rules are active without running `/lotokens` again.

- Only the rules for the functions you selected are written — unused functions are omitted.
- If a `## LoTokens` block already exists in the file, it is replaced entirely.
- To update preferences: run `/lotokens` again and choose new options.
- To remove preferences: delete the `## LoTokens` block from the corresponding `CLAUDE.md`, or run `/lotokens` and select no functions.

**OS detection:** Claude detects your operating system automatically and uses the correct path. On Windows, `%USERPROFILE%` is expanded to your home directory (e.g. `C:\Users\yourname`).

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

# Skill-LoTokens — Documentacion en Espanol

Una skill para Claude Code que reduce el uso de tokens en tus sesiones. Activa solo lo que necesitas desde un menu interactivo. Guarda tus preferencias para que persistan entre sesiones.

---

## Funciones

| Funcion | Que hace |
|---|---|
| **Bloquear .md** | Impide que Claude cree o edite cualquier archivo `.md` en tu proyecto |
| **Sin emojis** | Elimina emojis de todas las respuestas y del codigo generado |
| **Respuesta corta** | Al completar cualquier tarea (uso de herramientas), Claude responde unicamente: `Listo` |

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
| **Guardar globalmente** | Las reglas se escriben en `~/.claude/CLAUDE.md` (Linux/macOS) o `%USERPROFILE%\.claude\CLAUDE.md` (Windows) y aplican en todos los proyectos |
| **Guardar para este proyecto** | Las reglas se escriben en `.claude/CLAUDE.md` del directorio actual y aplican solo aqui |

### Como funciona la memoria persistente

Al guardar, Claude escribe un bloque `## LoTokens` en el archivo `CLAUDE.md` correspondiente. Claude Code carga `CLAUDE.md` automaticamente al iniciar cada sesion, por lo que tus reglas quedan activas sin necesidad de volver a ejecutar `/lotokens`.

- Solo se escriben las reglas de las funciones que seleccionaste — las no utilizadas se omiten.
- Si ya existe un bloque `## LoTokens` en el archivo, se reemplaza por completo.
- Para cambiar preferencias: ejecuta `/lotokens` nuevamente y elige nuevas opciones.
- Para eliminar preferencias: borra el bloque `## LoTokens` del `CLAUDE.md` correspondiente, o ejecuta `/lotokens` sin seleccionar ninguna funcion.

**Deteccion de sistema operativo:** Claude detecta tu sistema operativo automaticamente y usa la ruta correcta. En Windows, `%USERPROFILE%` se expande a tu directorio de usuario (por ejemplo `C:\Users\tunombre`).

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
