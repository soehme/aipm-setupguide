# Codex Basics

## Was ist Codex?

Codex ist der KI-Assistent von OpenAI für die Kommandozeile. Du gibst Aufgaben in natürlicher Sprache ein, und Codex arbeitet direkt mit deinen Dateien -- lesen, schreiben, analysieren, erklären.

## Starten und Beenden

```
codex                 # Codex starten
/exit                 # Beenden (auch /quit)
```

Codex startet im aktuellen Verzeichnis. Wechsle vorher in den richtigen Ordner:
```
cd ~/aipm
codex
```

Für die Arbeit im Training startest du mit gesetzten Berechtigungen:
```
codex -s workspace-write -a on-request
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
| `/exit`, `/quit` | Codex beenden |
| `/status` | Modell, Anbieter, Berechtigungen und Token-Nutzung der Sitzung |
| `/permissions` | Berechtigungen umschalten, ohne Codex neu zu starten |
| `/model` | Modell wechseln (welche zur Auswahl stehen, hängt vom Anbieter ab) |
| `/compact` | Verlauf zusammenfassen, wenn das Gespräch sehr lang wird |
| `/skills` | Verfügbare Skills auflisten und auswählen |
| `/mcp` | Angebundene externe Werkzeuge anzeigen |
| `/plugins` | Installierte Plugins anzeigen und verwalten |
| `/init` | Gerüst für eine `AGENTS.md` im Projekt erzeugen |
| `/review` | Änderungen im Arbeitsordner prüfen lassen |

Dazu ein paar Befehle für die Kommandozeile selbst -- also außerhalb einer laufenden Sitzung:

```
codex --version      # installierte Version
codex doctor         # Selbstdiagnose: Installation, Config, Anmeldung, Rechte
codex login status   # bin ich angemeldet, und wie?
codex resume         # frühere Sitzung fortsetzen
```

## Berechtigungen: der Modus statt der Einzelfrage

Codex fragt nicht vor jeder Dateiänderung. Es arbeitet in einem Modus, den du vorher setzt:

| Modus | Was Codex darf |
|---|---|
| `read-only` | nur lesen |
| `workspace-write` | im Arbeitsordner lesen und schreiben, Netzwerk gesperrt |
| `danger-full-access` | alles, ohne Schutz |

Dazu die Freigabe-Regel: `on-request` (Codex fragt, wenn es über den Arbeitsordner hinaus will) oder `never` (fragt nie).

Für die Arbeit im Training: `workspace-write` plus `on-request`. `/status` zeigt dir jederzeit, was gerade gilt, `/permissions` schaltet um.

> **Der Startordner ist kein Sicherheitszaun.** Er setzt den praktischen Fokus -- was Codex tatsächlich lesen und schreiben darf, entscheidet der Modus. Die Arbeitsregel bleibt trotzdem sinnvoll: ein Thema, ein Ordner, Codex dort starten.

## Bilder mitgeben

Ein Bild kannst du im Eingabefeld mit `Ctrl+V` einfügen -- auch auf dem Mac, nicht `Cmd+V`. Ob das klappt, hängt vom Terminal ab. Zuverlässiger ist der Weg über den Start:

```
codex -i screenshot.png
```

## Tipps

- **Sei konkret:** "Lies die Datei X und fasse den Inhalt in 3 Sätzen zusammen" funktioniert besser als "Mach was mit X".
- **Arbeitsverzeichnis:** Codex arbeitet in dem Ordner, in dem du es gestartet hast. Starte es dort, wo deine Dateien liegen.
- **Dateien benennen:** Nenne den genauen Pfad, z.B. `help/codex/codex-config.md`.
- **Geduld:** Manche Antworten dauern ein paar Sekunden -- Codex liest und denkt nach.
- **Nachfragen:** Wenn die Antwort nicht passt, frag einfach anders oder präziser nach.

## Sicherheit

- Deine Dateien verlassen nicht deinen Computer (nur der Text der Anfrage geht an den Anbieter)
- Änderungen kannst du über `git` oder eine Sicherungskopie rückgängig machen
- `danger-full-access` und `--dangerously-bypass-approvals-and-sandbox` sind kein Arbeitsmodus, sondern eine Notlösung für Sonderfälle
