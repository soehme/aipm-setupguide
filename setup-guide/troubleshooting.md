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

**1. Aktuelle Version prüfen:**

**Mac (Terminal):**
```
python3 --version
```

**Windows (PowerShell):**
```
python --version
```

**2. Python aktualisieren:**

**Mac (Homebrew):**
```
brew install python3
```

Alternativ: [python.org/downloads](https://www.python.org/downloads/)

**Windows:**
```
winget install Python.Python.3.13
```

Alternativ: [python.org/downloads](https://www.python.org/downloads/) -- beim Installer unbedingt **"Add Python to PATH"** ankreuzen.

**3. Pfad zur neuen Python-Installation ermitteln:**

**Mac (Terminal):**
```
which python3
```

Typisches Ergebnis bei Homebrew: `/opt/homebrew/bin/python3`

**Windows (PowerShell):**
```
where python
```

**4. Pfad im Terminal-Plugin eintragen:**

1. Öffne die Einstellungen des Terminal-Plugins (Community Plugins -> Terminal -> Zahnrad-Symbol)
2. Gehe zu **"Profiles"** und klicke auf **"Edit"** beim passenden integrierten Profil:
   - Mac: `darwinIntegratedDefault`
   - Windows: `win32IntegratedDefault`
   - Linux: `linuxIntegratedDefault`
3. Trage unter **"Python executable"** den Pfad aus Schritt 3 ein -- inklusive `python.exe` am Ende, z.B. `C:\Python312\python.exe`
4. Schließe die Einstellungen und öffne ein neues Terminal

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
