# Troubleshooting (Claude Code und Codex)

Diese Datei sammelt Probleme, die unabhängig vom eingesetzten Tool auftreten -- beim Klonen, bei Node.js und beim Terminal-Plugin in Obsidian. Tool-spezifische Probleme stehen in der Troubleshooting-Datei im Ordner deines Tools (`claude/` bzw. `codex/`).

## "git" wird nicht erkannt (Windows)

Die Fehlermeldung `Die Benennung "git" wurde nicht als Name eines Cmdlet erkannt` bedeutet: Git ist auf diesem Computer nicht installiert.

**Option 1: Git installieren (empfohlen)**

1. Lade Git für Windows herunter: [git-scm.com/download/win](https://git-scm.com/download/win)
2. Installiere Git (alle Standardoptionen übernehmen)
3. Schließe PowerShell und öffne sie neu
4. Führe den `git clone`-Befehl aus Schritt 1 nochmal aus

**Option 2: Repository manuell herunterladen (ohne Git)**

Falls du Git nicht installieren möchtest oder kannst:

1. Öffne im Browser: `https://github.com/soehme/aipm-setupguide`
2. Klicke auf den grünen Button **"Code"** → **"Download ZIP"**
3. Entpacke die ZIP-Datei (Rechtsklick → Alle extrahieren)
4. Benenne den entpackten Ordner um zu `aipm`
5. Verschiebe ihn in dein Home-Verzeichnis: `C:\Users\DeinName\aipm`

---

## "npm" oder "node" wird nicht erkannt (Windows)

Die Fehlermeldung `Die Benennung "npm" wurde nicht als Name eines Cmdlet erkannt` bedeutet: Node.js ist nicht installiert oder noch nicht im PATH registriert.

**Node.js installieren:**

1. Lade Node.js herunter: [nodejs.org/de/download](https://nodejs.org/de/download)
2. Installiere Node.js -- beim Setup-Assistenten den Haken bei **"Add to PATH"** nicht entfernen
3. Schließe PowerShell und öffne sie neu
4. Prüfe die Installation:
   ```
   node --version
   npm --version
   ```
5. Führe dann die Installation deines Tools aus Schritt 2 nochmal aus

---

## Terminal zeigt einen Python-Fehler

Wenn beim Öffnen eines Terminals in Obsidian eine der folgenden Meldungen erscheint:

```
Terminal resizer exited unexpectedly: 9009
```
```
ImportError: cannot import name 'Self' from 'typing' (…/python3.9/typing.py)
```

...fehlt Python entweder ganz, oder die installierte Version ist zu alt. Das Terminal-Plugin benötigt Python 3.10 oder neuer. Außerdem öffnet sich möglicherweise ein separates schwarzes Konsolenfenster -- das verschwindet nach dem Fix.

---

### Mac

**1. Version prüfen:**

```
python3 --version
```

**2. Python aktualisieren (falls nötig):**

```
brew install python3
```

Alternativ: [python.org/downloads](https://www.python.org/downloads/)

---

### Windows

Auf Windows gibt es zwei häufige Ursachen für den Fehler:

- **App-Ausführungsaliase** -- Windows legt Pseudo-Einträge für `python.exe` und `python3.exe` an, die auf den Microsoft Store verweisen statt auf die echte Installation. Das Terminal-Plugin ruft dann einen Store-Stub auf, der sofort fehlschlägt.
- **`python3.exe` fehlt** -- Das Terminal-Plugin ruft intern `python3` auf. Windows-Python-Installationen legen aber standardmäßig nur `python.exe` an, kein `python3.exe`.

**1. App-Ausführungsaliase deaktivieren:**

1. Windows-Taste → **Einstellungen → Apps → Erweiterte App-Einstellungen → App-Ausführungsaliase**
2. Dort beide Einträge ausschalten:
   - `python.exe`
   - `python3.exe`

**2. `python3.exe` anlegen:**

Falls Python 3.13 bereits installiert ist (prüfen mit `python --version`), kopiere die Datei:

```
Copy-Item "$env:LOCALAPPDATA\Programs\Python\Python313\python.exe" "$env:LOCALAPPDATA\Programs\Python\Python313\python3.exe" -Force
```

PowerShell danach schließen und neu öffnen.

**3. Installation prüfen:**

```
where.exe python
where.exe python3
python --version
python3 --version
```

Erwartetes Ergebnis (Pfade mit deinem Benutzernamen):

```
C:\Users\DeinName\AppData\Local\Programs\Python\Python313\python.exe
C:\Users\DeinName\AppData\Local\Programs\Python\Python313\python3.exe
Python 3.13.x
Python 3.13.x
```

> Wenn `where.exe python3` weiterhin einen `WindowsApps`-Pfad zuerst anzeigt, ist der Alias noch aktiv oder der Python-Pfad steht zu weit hinten in der PATH-Liste. Dann in den Umgebungsvariablen (Einstellungen → System → Umgebungsvariablen) diese beiden Einträge ganz nach oben schieben:
> ```
> C:\Users\DeinName\AppData\Local\Programs\Python\Python313
> C:\Users\DeinName\AppData\Local\Programs\Python\Python313\Scripts
> ```

**4. Obsidian neu starten:**

Obsidian komplett schließen -- im Task-Manager prüfen, dass `Obsidian.exe` nicht mehr läuft -- dann neu starten.

---

## Obsidian-Einstellungen manuell setzen

Der `aipm`-Ordner bringt vier Obsidian-Einstellungen schon mit (sie stehen in `.obsidian/app.json`, `.obsidian/appearance.json` und `.obsidian/snippets/`). Falls sie bei dir nicht greifen -- etwa weil du das Repository als ZIP ohne versteckte Ordner heruntergeladen oder einen anderen Ordner als Vault geöffnet hast -- kannst du sie von Hand setzen.

Öffne die Einstellungen mit `Cmd+,` (Mac) bzw. `Ctrl+,` (Windows):

**Files & Links:**
- "Default location for new attachments" auf **"In subfolder under current folder"** setzen
- Subfolder name: `attachments`
- "Show all file types" aktivieren -- damit zeigt der Dateibrowser nicht nur Markdown-Dateien, sondern alle Dateitypen an

**Appearance:**
- "Inline title" deaktivieren -- sonst wird der Dateiname doppelt angezeigt (im Tab und nochmal groß im Editor)
- Unter **"CSS snippets"** auf das Ordner-Symbol klicken, um den Snippet-Ordner zu öffnen
- Dort eine neue Datei `show-extensions.css` anlegen mit folgendem Inhalt:

```css
.nav-file-title-content::after {
  content: ".md";
  opacity: 0.5;
}
```

- Zurück in Obsidian unter CSS snippets auf das Refresh-Symbol (Pfeile) klicken, damit das neue Snippet erkannt wird
- Den Snippet **"show-extensions"** aktivieren -- damit wird die `.md`-Endung im Dateibrowser sichtbar

---

## Versteckte Ordner fehlen nach ZIP-Download

Beim Entpacken einer ZIP-Datei lässt Windows Ordner, die mit einem Punkt beginnen, manchmal weg. Dann fehlen `.obsidian` (die vorbereiteten Einstellungen) und `help/.versteckterOrdner` (der Testordner aus dem Setup).

Sauberste Lösung: das Repository stattdessen mit `git clone` holen (siehe oben). Alternativ im Explorer unter **Ansicht → Einblenden → Ausgeblendete Elemente** aktivieren und die fehlenden Ordner aus dem entpackten Archiv nachkopieren.

Funktioniert es immer noch nicht? Dann schau in die Troubleshooting-Datei im Ordner deines Tools (`claude/` bzw. `codex/`) -- dort steht für jedes Tool ein Plan B.
