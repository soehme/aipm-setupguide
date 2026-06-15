# Troubleshooting

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
5. Führe dann die Claude Code Installation aus Schritt 2 nochmal aus

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

Funktioniert es immer noch nicht? Dann weiter mit Plan B.

## Plan B (Windows): Claudian statt Terminal-Plugin

Wenn das Terminal-Plugin auf Windows nicht zuverlässig funktioniert, ist Claudian eine Alternative: ein Obsidian-Plugin, das Claude Code direkt als Chat-Interface in Obsidian einbettet -- ohne Terminal.

**1. Claudian via BRAT installieren:**

1. Öffne die BRAT-Einstellungen (Community Plugins -> BRAT -> Zahnrad-Symbol)
2. Klicke **"Add Beta plugin"**
3. Füge diese URL ein: `https://github.com/YishenTu/claudian`
4. Klicke **"Add Plugin"**
5. Aktiviere Claudian unter Community Plugins

**2. Claudian einrichten:**

1. Öffne die Claudian-Einstellungen (Community Plugins -> Claudian -> Zahnrad-Symbol)
2. Scrolle ganz nach unten zu **"Advanced"**
3. Aktiviere **"Enable bash mode (!)"**

**3. Claudian starten:**

1. Klicke auf das Roboter-Symbol (🤖) in der linken Symbolleiste
2. Stelle oben im Chat-Fenster ein:
   - Modell: **Sonnet**
   - Thinking: **Medium**
   - Modus: von **YOLO** auf **Safe** umstellen

> **Hinweis:** Im Safe-Modus fragt Claudian vor Dateiänderungen nach -- empfehlenswert für den Einstieg.
