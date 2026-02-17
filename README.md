# AIPM Setup Guide

Willkommen! Diese Anleitung hilft dir, deine Arbeitsumgebung für das Training einzurichten. Du brauchst **Claude Code** (ein KI-Assistent im Terminal) und **Obsidian** (ein komfortabler Editor für Textdateien).

Plane ca. 30 Minuten ein.

---

## Schritt 1: Ordner anlegen & Demo-Dateien holen

### Ordner anlegen

> **Neu bei der Kommandozeile?** Die Kommandozeile (auch Terminal genannt) ist ein Textfenster, in das du Befehle eintippst. Auf dem **Mac** findest du sie unter Programme → Dienstprogramme → Terminal (oder über Spotlight: `Cmd+Leertaste`, dann "Terminal" tippen). Unter **Windows** öffnest du PowerShell über das Startmenü (nach "PowerShell" suchen). Tippe den jeweiligen Befehl ein und drücke `Enter`, um ihn auszuführen.

Erstelle einen Ordner `aipm` in deinem Home-Verzeichnis:

**Mac (Terminal):**
```
mkdir ~/aipm
```

**Windows (PowerShell):**
```
mkdir $HOME\aipm
```

### Demo-Dateien herunterladen

Klone das Repository in deinen neuen Ordner:

```
git clone https://github.com/soehme/aipm-setupguide ~/aipm
```

Danach findest du in `~/aipm` mehrere Beispieldateien und Ordner, die wir im Training nutzen.

---

## Schritt 2: Claude Code installieren

### Was ist Claude Code?

Claude Code ist Anthropics KI-Assistent für die Kommandozeile. Du stellst Fragen oder gibst Aufgaben in natürlicher Sprache ein, und Claude arbeitet direkt mit deinen Dateien -- liest, schreibt, analysiert und erklärt.

### Installation

**Mac (empfohlen -- nativer Installer):**
```
curl -fsSL https://claude.ai/install.sh | bash
```

**Mac (alternativ -- Homebrew):**
```
brew install --cask claude-code
```

**Windows:**
```
npm install -g @anthropic-ai/claude-code
```
Voraussetzung: Node.js 18 oder neuer (`node --version` zum Prüfen).

### API-Zugang einrichten

Claude Code braucht einen Zugang zu Anthropic. Dafür gibt es zwei Wege:

1. **Claude Subscription** (empfohlen für Einzelpersonen) -- Melde dich bei claude.ai an und wähle ein Abo.
2. **API Key** (empfohlen für Unternehmen) -- Dein Unternehmen stellt dir einen API Key bereit. Trage ihn so ein:

```
export ANTHROPIC_API_KEY="dein-key-hier"
```

> Frag bei deinem Unternehmen nach, welchen Zugang du nutzen sollst, und richte ihn **vor dem Training** ein.

### Test: Funktioniert alles?

Starte Claude Code:
```
claude
```

Tippe dann:
```
Was ist 2 + 2?
```

Wenn du eine Antwort bekommst, ist alles eingerichtet. Beende mit `/exit`.

---

## Schritt 3: Obsidian installieren

### Was ist Obsidian?

Obsidian ist ein Editor für Markdown-Textdateien mit integriertem Dateibrowser. Für uns ist es die komfortable Oberfläche, in der wir Dateien verwalten, bearbeiten und mit KI arbeiten -- ohne Entwicklertools.

### Installation

1. Lade Obsidian herunter: [obsidian.md/download](https://obsidian.md/download)
2. Installiere die App (Mac: in den Applications-Ordner ziehen)

**Alternativ mit Homebrew (Mac):**
```
brew install --cask obsidian
```

### Vault öffnen

1. Starte Obsidian
2. Wähle **"Open folder as vault"** (Ordner als Vault öffnen)
3. Navigiere zu `~/aipm` und wähle den Ordner aus
4. Klicke **"Open"**

### Einstellungen vornehmen

Öffne die Einstellungen mit `Cmd+,` (Mac) bzw. `Ctrl+,` (Windows):

**Files & Links:**
- "Default location for new attachments" auf **"In subfolder under current folder"** setzen
- Subfolder name: `attachments`

### Oberfläche einrichten

- **Linke Sidebar:** Klicke auf das Ordner-Symbol oben links, um den Dateibrowser zu sehen. Hier siehst du alle Dateien in deinem Vault.
- **Rechte Sidebar:** Schließe sie mit Klick auf den Pfeil, um mehr Platz zu haben.

### Test: Erste Datei erstellen

1. Drücke `Cmd+N` (Mac) bzw. `Ctrl+N` (Windows) für eine neue Datei
2. Gib ihr einen Namen, z.B. "Meine erste Notiz"
3. Schreibe ein paar Zeilen Text
4. Finde die Datei im Finder/Explorer unter `~/aipm/`
5. Lösche die Testdatei wieder (Rechtsklick in Obsidian -> Delete)

---

## Schritt 4: Obsidian Plugins installieren

### Community Plugins aktivieren

1. Öffne Einstellungen (`Cmd+,`)
2. Gehe zu **Community Plugins**
3. Klicke **"Turn on community plugins"**

### Plugin 1: Terminal

Damit kannst du ein Terminal direkt in Obsidian öffnen -- dort läuft dann Claude Code.

1. In Community Plugins auf **"Browse"** klicken
2. Nach **"Terminal"** suchen
3. **"Install"** und dann **"Enable"** klicken

### Plugin 2: BRAT

BRAT erlaubt die Installation von Plugins, die nicht im offiziellen Verzeichnis stehen.

1. In Community Plugins auf **"Browse"** klicken
2. Nach **"BRAT"** suchen
3. **"Install"** und dann **"Enable"** klicken

### Plugin 3: Show Hidden Files (via BRAT)

Dieses Plugin zeigt versteckte Dateien und Ordner (die mit `.` beginnen) im Dateibrowser an.

1. Öffne die Einstellungen von BRAT (unter Community Plugins -> BRAT -> Zahnrad-Symbol)
2. Klicke **"Add Beta plugin"**
3. Füge diese URL ein: `https://github.com/polyipseity/obsidian-show-hidden-files`
4. Klicke **"Add Plugin"**
5. Aktiviere das Plugin unter Community Plugins

> **Hinweis:** Falls dein Vault sehr große versteckte Ordner enthält (z.B. `.git` mit vielen Dateien), kann Obsidian kurz langsamer werden.

### Test: Alles eingerichtet?

- Öffne ein Terminal in Obsidian (Command Palette: `Cmd+P`, dann "terminal current integrated" tippen)
- Prüfe, ob du den Ordner `.versteckterOrdner` im Dateibrowser als Unterordner von `help` siehst (Show Hidden Files Plugin)

---

## Geschafft!

Super, du bist eingerichtet. Freu dich aufs Training!

In deinem `~/aipm`-Ordner findest du:
- `help/` -- Hilfsdateien zu Markdown, Obsidian und Claude Code
- `leihsdir/` -- Beispieldaten für Übungen

Schau gerne auch schonmal diese Dateien an, um etwas besser zu verstehen, was du gerade eingerichtet hast:
1. [[obsidian-basics]]
2. [[markdown-basics]]
3. [[claudecode-basics]]
4. [[atsign]]

Bei Fragen melde dich gerne vor dem Training.
