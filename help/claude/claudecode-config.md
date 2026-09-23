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
└── plugins/                      ← installierte Plugins
    └── ...

~/aipm/                           ← Projektordner (Beispiel)
├── CLAUDE.md                     ← Projektanweisungen (geht mit in Repo)
├── CLAUDE.local.md               ← Projektanweisungen (bleibt lokal)
├── .mcp.json                     ← MCP-Server für dieses Projekt
└── .claude/                      ← projektlokale Ebene
    ├── settings.json             ← projektlokale Einstellungen & Berechtigungen
    └── skills/                   ← Skills (nur dieses Projekt)
        └── mein-skill/
            └── SKILL.md
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

### Skills aufrufen

Es gibt zwei Wege, einen Skill zu nutzen:

**Implizit** -- du beschreibst deine Aufgabe ganz normal, und Claude erkennt anhand der `description`, dass ein Skill dazu passt, und nutzt ihn von selbst. Dafür muss die `description` gut sein: Sie soll beschreiben, *wann* der Skill dran ist, nicht nur was er tut.

**Explizit** -- du rufst den Skill direkt beim Namen auf:

```
/mein-skill              # eigener Skill
/plugin-name:skill-name  # Skill aus einem Plugin
```

Explizit ist zuverlässiger, implizit ist bequemer. Im Training schauen wir uns beides an.

> **Was ist mit Slash-Commands?** Früher gab es dafür einzelne `.md`-Dateien in einem `commands/`-Ordner. Das funktioniert weiterhin, ist für neue Sachen aber nicht mehr der richtige Weg: Skills können dasselbe, nehmen zusätzlich Referenzdateien auf und werden auch von anderen Werkzeugen gelesen. Leg Neues als Skill an.

## Plugins

Plugins sind **installierbare Pakete**, die Skills und MCP-Server bündeln. Sie werden über den Plugin-Marketplace verteilt und unter `~/.claude/plugins/` installiert.

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
