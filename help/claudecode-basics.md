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
| `/help` | Hilfe anzeigen |
| `/exit` | Claude Code beenden |
| `/clear` | Bisherigen Gesprächsverlauf löschen |
| `/status` | Aktuellen Status und Authentifizierung anzeigen |

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
