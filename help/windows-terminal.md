# Windows Terminal Basics

## Was ist PowerShell?

PowerShell ist die Kommandozeile von Windows -- ein Textfenster, in dem du Befehle eingibst, statt auf Symbole zu klicken. Claude Code läuft hier.

## PowerShell starten

- **Windows-Taste** drücken, `PowerShell` tippen, Enter
- Oder: Rechtsklick auf Start-Symbol → "Terminal" oder "Windows PowerShell"

> **Tipp:** Suche nach "Windows Terminal" -- das ist die modernere Variante und öffnet PowerShell standardmäßig.

## Die wichtigsten Befehle

| Befehl | Bedeutung | Beispiel |
|--------|-----------|---------|
| `pwd` | Aktuellen Ordner anzeigen | `pwd` |
| `ls` | Inhalt des aktuellen Ordners anzeigen | `ls` |
| `cd Ordner` | In einen Ordner wechseln | `cd aipm` |
| `cd ..` | Einen Ordner zurück | `cd ..` |
| `cd ~` | In den Home-Ordner wechseln | `cd ~` |
| `mkdir Name` | Neuen Ordner erstellen | `mkdir aipm` |
| `cls` | Bildschirm leeren | `cls` |

## Pfade verstehen

- `~` ist dein persönlicher Ordner, z.B. `C:\Users\deinname`
- `~/aipm` bedeutet also `C:\Users\deinname\aipm`
- Mit **Tab** ergänzt PowerShell Ordner- und Dateinamen automatisch

## Typischer Ablauf

```
cd ~/aipm          # in deinen Arbeitsordner wechseln
ls                 # prüfen, was darin liegt
claude             # Claude Code starten
```

> **Hinweis:** Wenn ein Befehl nicht funktioniert, prüfe zuerst mit `pwd`, ob du im richtigen Ordner bist.
