# Claude Code Basics

## Was ist Claude Code?

Claude Code ist ein KI-Assistent für die Kommandozeile von Anthropic. Du gibst Aufgaben in natürlicher Sprache ein, und Claude arbeitet direkt mit deinen Dateien -- lesen, schreiben, analysieren, erklären.

## Starten und Beenden

```
claude                # Claude Code starten
/exit                 # Beenden
```

Claude startet im aktuellen Verzeichnis. Wechsle vorher in den richtigen Ordner:
```
cd ~/aipm
claude
```

## Grundlegende Nutzung

Tippe einfach deine Frage oder Aufgabe ein:

```
> Was steht in der Datei leihsdir/leihsdir-context.md?
> Fasse alle Markdown-Dateien in diesem Ordner zusammen.
> Erstelle eine neue Datei namens notizen.md mit einer Einkaufsliste.
```

## Wichtige Slash-Befehle

| Befehl | Beschreibung |
|--------|-------------|
| `/help` | Alle Befehle anzeigen |
| `/exit` | Claude Code beenden |
| `/clear` | Gesprächsverlauf löschen -- nützlich, wenn Claude "verwirrt" wirkt |
| `/compact` | Kontext zusammenfassen, wenn das Gespräch sehr lang wird |
| `/model` | Modell wechseln (z.B. auf Opus oder Haiku) |
| `/cost` | Verbrauchte Tokens und Kosten der aktuellen Session anzeigen |
| `/status` | Auth-Status und aktuelle Einstellungen prüfen |

## Dateien und URLs mit @ einbinden

Mit `@` kannst du Dateien oder Webseiten direkt in deinen Prompt einbinden:

```
> @help/markdown-basics.md -- erkläre mir die wichtigsten Formatierungen
> @https://example.com/artikel -- fasse diesen Artikel zusammen
```

Claude liest den Inhalt dann automatisch mit. Das ist nützlicher als "schau mal in die Datei X", weil Claude den Kontext direkt bekommt.

> **Tipp:** Nach dem `@` kannst du den Dateinamen tippen und mit Tab ergänzen lassen.

## Tipps

- **Sei konkret:** "Lies die Datei X und fasse den Inhalt in 3 Sätzen zusammen" funktioniert besser als "Mach was mit X".
- **Arbeitsverzeichnis:** Claude arbeitet im Ordner, in dem du es gestartet hast. Starte es dort, wo deine Dateien liegen.
- **Dateien benennen:** Wenn du Dateien meinst, nenne den genauen Pfad, z.B. `help/setup-guide.md`.
- **Geduld:** Manche Antworten dauern ein paar Sekunden -- Claude liest und denkt nach.
- **Nachfragen:** Wenn die Antwort nicht passt, frag einfach anders oder präziser nach.

## Sicherheit

- Claude fragt um Erlaubnis, bevor es Dateien verändert oder Befehle ausführt
- Du kannst einzelne Aktionen ablehnen
- Deine Dateien verlassen nicht deinen Computer (nur der Text der Anfrage geht an die API)
