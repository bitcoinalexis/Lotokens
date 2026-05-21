# Skill-LoTokens

A Claude Code skill to reduce token usage during your sessions. Activate only what you need from an interactive menu.

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

An interactive menu will appear. Select the functions you want to activate for the current session.

---

## Example

```
/lotokens

LoTokens — select the functions you want to activate:
  [x] No emojis
  [x] Short response
  [ ] Block .md

LoTokens active — No emojis | Short response
```

---

## Compatibility

- Claude Code CLI
- Claude Code desktop app
- Claude Code IDE extensions (VS Code, JetBrains)

---

Built for [Claude Code](https://claude.ai/code) by AngyLabs.
