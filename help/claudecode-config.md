# Claude Code: Konfiguration & Struktur

Claude Code organisiert sich in zwei Ebenen: **global** (gilt für alle Projekte) und **projektlokal** (gilt nur im aktuellen Ordner). Projektlokale Einstellungen überschreiben globale.

## Übersicht

```
~/.claude.json                    ← globale MCP-Server-Konfiguration
~/.claude/                        ← globale Ebene (immer aktiv)
├── CLAUDE.md                     ← globale Anweisungen für Claude
├── settings.json                 ← Einstellungen & Berechtigungen
├── skills/                       ← eigene Skills
│   └── mein-skill/
│       └── SKILL.md
├── commands/                     ← eigene Slash-Commands
│   └── meinbefehl.md
└── plugins/                      ← installierte Plugins
    └── ...

~/aipm/                           ← Projektordner (Beispiel)
├── CLAUDE.md                     ← Projektanweisungen (geht mit in Repo)
├── CLAUDE.local.md               ← Projektanweisungen (bleibt lokal)
├── .mcp.json                     ← MCP-Server für dieses Projekt
└── .claude/                      ← projektlokale Ebene
    ├── settings.json             ← projektlokale Einstellungen & Berechtigungen
    ├── skills/                   ← Skills (nur dieses Projekt)
    │   └── mein-skill/
    │       └── SKILL.md
    └── commands/                 ← Slash-Commands (nur dieses Projekt)
        └── meinbefehl.md
```

## Die wichtigsten Dateien

### CLAUDE.md -- Anweisungen für Claude

Claude liest `CLAUDE.md` automatisch beim Start. Hier steht, wie Claude sich verhalten soll: Tonalität, Konventionen, Hintergrundinformationen zum Projekt.

Es gibt drei:
- `~/.claude/CLAUDE.md` -- gilt immer, für alle Projekte
- `CLAUDE.md` im Projektordner -- gilt nur in diesem Projekt
- `CLAUDE.local.md`im Projektordner -- gilt nur in diesem Projektund wird nicht in Git-Repositories eingecheckt.

## Skills

Skills sind spezialisierte Wissenspakete, die Claude für bestimmte Aufgaben nutzen kann. Jeder Skill ist ein **Ordner mit einer `SKILL.md`** darin:

```
mein-skill/
└── SKILL.md           ← Pflichtdatei mit Name, Beschreibung und Anweisungen
```

Die `SKILL.md` beginnt mit einem YAML-Header:

```
---
name: mein-skill
description: "Kurze Beschreibung, wann dieser Skill genutzt werden soll."
---

# Mein Skill

Hier stehen die detaillierten Anweisungen für Claude...
```

Skills können auch weitere Referenzdateien im selben Ordner enthalten (z.B. Vorlagen, Muster, Beispiele).

**Eigene Skills** legst du an unter:
- `~/.claude/skills/` -- gelten für alle Projekte
- `.claude/skills/` im Projektordner -- gelten nur dort

Skills können auch über Plugins installiert werden (siehe unten).

### commands/ -- eigene Slash-Commands

Einzelne `.md`-Dateien im `commands/`-Ordner werden zu Slash-Commands. Der Dateiname wird zum Befehlsnamen:

```
~/.claude/commands/zusammenfassen.md  →  /zusammenfassen  (global)
.claude/commands/zusammenfassen.md    →  /zusammenfassen  (projektlokal)
```

Der Inhalt der Datei ist der Prompt, den Claude bei Aufruf des Befehls ausführt.

> **Hinweis:** Für umfangreichere Befehle mit Referenzdateien sind Skills unter `skills/` die bessere Wahl.

## Plugins

Plugins sind **installierbare Pakete**, die Skills, Commands und MCP-Server bündeln. Sie werden über den Plugin-Marketplace verteilt und unter `~/.claude/plugins/` installiert.

Ein Plugin enthält typischerweise:

```
mein-plugin/
├── .claude-plugin/
│   └── plugin.json        ← Name, Version, Autor, Beschreibung
├── skills/                ← ein oder mehrere Skills
│   ├── skill-a/
│   │   └── SKILL.md
│   └── skill-b/
│       └── SKILL.md
└── .mcp.json              ← MCP-Server des Plugins
```

```
/plugins         # installierte Plugins anzeigen und verwalten
```

Skills aus Plugins werden mit Namespace aufgerufen: `/plugin-name:skill-name`.

Beispiele für Plugins: Document Skills (PDF, PPTX, XLSX erstellen), PM-Skills (PRDs, OKRs, User Stories), Miro-Integration.

## MCP-Server (externe Tools)

MCP (Model Context Protocol) erlaubt es, externe Tools an Claude anzubinden -- z.B. Datenbanken, APIs oder andere Anwendungen. Die Konfiguration erfolgt über:
- `~/.claude.json` unter `mcpServers` -- gilt für alle Projekte (global)
- `.mcp.json` im Projektordner -- gilt nur für dieses Projekt
- MCP-Server können auch als Teil von Plugins mitgeliefert werden

```
/mcp             # angebundene MCP-Server anzeigen und verwalten
```

> **Tipp:** Du musst diese Dateien nicht von Hand anlegen. Claude kann das für dich tun -- frag einfach: "Erstelle eine CLAUDE.md in diesem Ordner mit folgenden Anweisungen: ..."
