# Codex: Konfiguration & Struktur

Codex organisiert sich in zwei Ebenen: **global** (gilt für alle Projekte) und **projektlokal** (gilt nur im aktuellen Ordner). Projektlokale Anweisungen ergänzen die globalen.

## Übersicht

```
~/.codex/                         ← globale Ebene
├── AGENTS.md                     ← globale Anweisungen für Codex
├── AGENTS.override.md            ← ersetzt AGENTS.md, wenn vorhanden
├── config.toml                   ← Modell, Anbieter, Rechte, MCP-Server
├── prompts/                      ← alte Custom Prompts (veraltet)
└── plugins/                      ← installierte Plugins

~/.agents/
└── skills/                       ← eigene Skills, gelten überall
    └── mein-skill/
        └── SKILL.md

~/aipm/                           ← Projektordner (Beispiel)
├── AGENTS.md                     ← Projektanweisungen
├── unterordner/AGENTS.md         ← zusätzliche Regeln für einen Teilbereich
└── .agents/
    └── skills/                   ← Skills nur für dieses Projekt
        └── mein-skill/
            └── SKILL.md
```

## AGENTS.md -- Anweisungen für Codex

Codex liest `AGENTS.md` automatisch beim Start. Hier steht, wie Codex sich verhalten soll: Tonalität, Konventionen, Hintergrundinformationen zum Projekt. Die Datei heißt bei anderen Werkzeugen genauso -- sie ist ein offener Standard und nicht an Codex gebunden. Bei Claude Code heißt das Gegenstück `CLAUDE.md`.

Codex sammelt die Anweisungen als Kette: erst die globale Datei aus `~/.codex/`, dann vom Projekt-Wurzelverzeichnis abwärts bis zu dem Ordner, in dem du gerade arbeitest. Pro Ebene zählt eine Datei. Was näher an deinem Arbeitsordner liegt, hat Vorrang.

Das lohnt sich zu nutzen: Allgemeines (Sprache, Ablage) gehört nach oben, Spezielles in den Unterordner, für den es gilt. Die zusammengesetzten Anweisungen sind auf 32 KiB begrenzt -- eine immer längere Wurzeldatei läuft irgendwann in diese Grenze.

`/init` erzeugt dir ein Gerüst.

## Skills -- wiederverwendbare Arbeitsabläufe

Skills sind Wissenspakete, die Codex für bestimmte Aufgaben nutzt. Jeder Skill ist ein **Ordner mit einer `SKILL.md`** darin:

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

Hier stehen die detaillierten Anweisungen für Codex...
```

Weitere Dateien im selben Ordner (Vorlagen, Beispiele, Muster) werden erst geladen, wenn sie gebraucht werden.

**Eigene Skills** legst du an unter:
- `~/.agents/skills/` -- gelten für alle Projekte
- `.agents/skills/` im Projektordner -- gelten nur dort

In einem Git-Repository sucht Codex von deinem aktuellen Ordner aufwärts bis zur Wurzel nach `.agents/skills`-Ordnern. Dadurch können Skills für ein ganzes Produkt oder nur für einen Teilbereich gelten.

### Skills aufrufen

Es gibt zwei Wege:

**Implizit** -- du beschreibst deine Aufgabe ganz normal, und Codex erkennt anhand der `description`, dass ein Skill dazu passt. Dafür muss die `description` gut sein: Sie soll beschreiben, *wann* der Skill dran ist, nicht nur was er tut.

**Explizit** -- du rufst den Skill direkt beim Namen auf:

```
$mein-skill
```

Oder du öffnest mit `/skills` die Liste und wählst aus.

Explizit ist zuverlässiger, implizit ist bequemer. Im Training schauen wir uns beides an.

> **Skill angelegt, aber nicht da?** Prüfe, ob es wirklich ein Ordner mit `SKILL.md` darin ist -- eine einzelne `.md`-Datei reicht nicht. Hilft das nicht, beende Codex mit `/exit` und starte neu.

> **Was ist mit Custom Prompts?** In `~/.codex/prompts/` liegen einzelne `.md`-Dateien, die sich als `/prompts:name` aufrufen lassen. Das ist der Vorgänger der Skills und veraltet. Leg Neues als Skill an.

## config.toml -- Einstellungen

Modell, Anbieter, Berechtigungen und MCP-Server stehen in `~/.codex/config.toml`. Das Format ist TOML, nicht JSON:

```toml
model = "gpt-5-codex"
approval_policy = "on-request"
sandbox_mode = "workspace-write"
```

> **Achtung:** Eine `config.toml` im Projektordner wird nicht verlässlich geladen (geprüft mit Version 0.155.1). Verlass dich für die Berechtigungen nicht darauf, sondern setz sie beim Start (`codex -s workspace-write -a on-request`) und prüf sie mit `/status`.

Was gerade tatsächlich gilt, zeigt dir `codex doctor` -- inklusive der Frage, aus welcher Datei die Konfiguration stammt.

## Plugins

Plugins bündeln Skills und MCP-Server zu einem installierbaren Paket:

```
/plugins                                  # in der Sitzung anzeigen und verwalten
codex plugin list                         # verfügbare Plugins
codex plugin add <plugin>@<marketplace>   # installieren
codex plugin marketplace add <quelle>     # Quelle hinzufügen
```

Nach einer Installation braucht Codex eine neue Sitzung, bevor die enthaltenen Skills und Werkzeuge verfügbar sind.

> **Nicht wahllos installieren.** Ein Plugin bringt fremde Anweisungen in deine Umgebung. Installiere nur aus Quellen, die du kennst. In Unternehmen ist der Katalog oft ohnehin eingeschränkt -- frag im Zweifel deinen Admin.

## MCP-Server (externe Werkzeuge)

MCP (Model Context Protocol) bindet externe Werkzeuge an -- Datenbanken, Jira, Miro und anderes. Am einfachsten über die Kommandozeile:

```
codex mcp add beispiel -- npx -y @anbieter/mcp-server
codex mcp list
```

Ein entfernter Server:

```
codex mcp add jira --url https://mcp.example.com/jira
codex mcp login jira
```

In der `config.toml` sieht ein Eintrag so aus:

```toml
[mcp_servers.jira]
url = "https://mcp.example.com/jira"
auth = "oauth"
```

Angebundene Server zeigt `/mcp` in der laufenden Sitzung.

> **Tipp:** Du musst diese Dateien nicht von Hand anlegen. Codex kann das für dich tun -- frag einfach: "Erstelle eine AGENTS.md in diesem Ordner mit folgenden Anweisungen: ..."
