# Troubleshooting (Codex)

Probleme, die nur Codex betreffen. Alles rund um git, Node.js, Obsidian-Einstellungen und das Terminal-Plugin steht in [troubleshooting.md](../troubleshooting.md) eine Ebene höher.

---

## Erste Maßnahme: codex doctor

Codex bringt eine eigene Diagnose mit. Sie prüft Installation, Konfiguration, Anmeldung, Berechtigungen und angebundene Werkzeuge in einem Durchgang:

```
codex doctor
```

Die Ausgabe ist lang. Interessant sind die Zeilen mit `⚠` oder `✗` -- dort steht meist direkt, was zu tun ist. Bei einem Problem lohnt sich dieser Befehl immer zuerst.

---

## "codex" wird nicht erkannt

Die Fehlermeldung `command not found: codex` (Mac) bzw. `Die Benennung "codex" wurde nicht als Name eines Cmdlet erkannt` (Windows) bedeutet: Codex ist nicht installiert oder nicht im PATH.

**Mac:**

```
brew install --cask codex
```

**Windows:**

```
npm install -g @openai/codex
```

Voraussetzung unter Windows ist Node.js 18 oder neuer. Fehlt auch `npm`, steht die Lösung in [troubleshooting.md](../troubleshooting.md).

Danach Terminal bzw. PowerShell schließen und neu öffnen.

---

## Anmeldung schlägt fehl

Prüfe zuerst, ob und wie du angemeldet bist:

```
codex login status
```

Welcher Anmeldeweg bei euch gilt, hängt vom Unternehmen ab -- ChatGPT-Account, API Key oder ein eigener Anbieter. Frag im Zweifel deinen Admin, bevor du etwas umstellst.

> **Hinweis:** Nutzt dein Unternehmen einen eigenen Anbieter (etwa einen Proxy oder Azure), ist die Anmeldung bei OpenAI selbst gar nicht nötig. `codex doctor` schreibt in dem Fall "OpenAI auth is not required for the active model provider" -- das ist kein Fehler.

---

## Kein passendes Modell in /model

Welche Modelle in `/model` auftauchen, hängt vom eingestellten Anbieter ab. Bei einem eigenen Unternehmens-Anbieter sieht die Liste anders aus als bei einem ChatGPT-Account. Ist die Liste leer oder unerwartet, prüfe mit `/status`, welcher Anbieter gerade aktiv ist, und frag deinen Admin nach dem vorgesehenen Modellnamen.

---

## Codex fragt nicht nach, bevor es Dateien ändert

Codex arbeitet nicht mit einer Rückfrage pro Dateioperation, sondern mit einem Modus, den du vorab setzt. Welcher gerade gilt, zeigt:

```
/status
```

Umschalten kannst du jederzeit in der laufenden Sitzung:

```
/permissions
```

Für den Einstieg passt `workspace-write` zusammen mit `on-request`: Codex darf im Arbeitsordner lesen und schreiben und fragt, wenn es darüber hinaus will. Details im [Codex Basics](../../help/codex/codex-basics.md).

---

## Skills werden nicht gefunden

Codex sucht Skills unter `~/.agents/skills/` (für alle Projekte) und `.agents/skills/` im Projektordner. Jeder Skill ist ein **Ordner** mit einer Datei `SKILL.md` darin -- eine einzelne `.md`-Datei ohne Ordner wird nicht erkannt.

Tauchen neu angelegte Skills nicht in `/skills` auf, beende Codex mit `/exit` und starte es neu.

---

## Plan B 1: Claudian statt Terminal-Plugin

Wenn das Terminal-Plugin nicht zuverlässig läuft -- das passiert vor allem unter Windows --, ist Claudian eine Alternative: ein Obsidian-Plugin, das Codex direkt als Chat-Fenster in Obsidian einbettet, ohne Terminal. Der Name klingt nach Claude, das Plugin unterstützt aber auch Codex.

**1. Claudian installieren:**

1. Einstellungen -> Community Plugins -> **"Browse"**
2. Nach **"Claudian"** suchen
3. Achte auf den Autor **Yishen Tu** -- es gibt mehrere ähnlich benannte Abwandlungen von anderen Autoren
4. **"Install"** und dann **"Enable"** klicken

**2. Claudian einrichten:**

1. Öffne die Claudian-Einstellungen (Community Plugins -> Claudian -> Zahnrad-Symbol)
2. Wähle als Agent **Codex**
3. Scrolle ganz nach unten zu **"Advanced"** und aktiviere **"Enable bash mode (!)"**

**3. Claudian starten:**

1. Klicke auf das Roboter-Symbol in der linken Symbolleiste
2. Stelle oben im Chat-Fenster den Modus von **YOLO** auf **Safe** um

> **Warum Safe?** Im Safe-Modus fragt Claudian vor Dateiänderungen nach -- genau das wollen wir im Training sehen. Den Sandbox-Modus von Codex selbst prüfst du weiterhin mit `/status`.

---

## Plan B 2: Codex im eigenen Terminal

Hilft auch Claudian nicht, arbeite vorerst mit zwei Fenstern nebeneinander:

1. Obsidian als Dateibrowser und Editor
2. Windows Terminal bzw. PowerShell oder das Mac-Terminal, darin `cd ~/aipm` (Windows: `cd $HOME\aipm`) und `codex`

Das ist unbequemer als die eingebettete Variante, funktioniert aber zuverlässig. Für das Training reicht es -- melde dich trotzdem vorher bei mir, dann schauen wir gemeinsam drauf.
