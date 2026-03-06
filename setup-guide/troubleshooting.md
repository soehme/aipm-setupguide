# Troubleshooting

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
3. Trage unter **"Python executable"** den Pfad aus Schritt 3 ein
4. Schließe die Einstellungen und öffne ein neues Terminal
