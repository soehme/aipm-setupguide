# Kommandozeilen-Basics

Die Kommandozeile (Terminal auf Mac, PowerShell auf Windows) ist ein Textfenster, in dem du Befehle eingibst statt auf Symbole zu klicken. Claude Code und viele andere Werkzeuge laufen hier.

> **Gut zu wissen:** PowerShell versteht die meisten Unix-Befehle (`ls`, `cd`, `pwd`, `cat`, ...) als Aliase. Die Beispiele hier funktionieren deshalb auf beiden Plattformen -- Unterschiede sind markiert.

---

## Wo bin ich? Wo will ich hin?

| Befehl | Beschreibung |
|--------|-------------|
| `pwd` | Aktuellen Ordner anzeigen (**p**rint **w**orking **d**irectory) |
| `cd Ordner` | In einen Ordner wechseln (**c**hange **d**irectory) |
| `cd ..` | Einen Ordner nach oben |
| `cd ~/aipm` | Direkt in den aipm-Ordner |
| `cd ~` | In den Home-Ordner |

```
pwd
# Mac:     /Users/deinname
# Windows: C:\Users\deinname

cd ~/aipm
pwd
# Mac:     /Users/deinname/aipm
# Windows: C:\Users\deinname\aipm

cd help
pwd
# Mac:     /Users/deinname/aipm/help
# Windows: C:\Users\deinname\aipm\help

cd ..
# Zurück in ~/aipm
```

> **Tipp:** Mit **Tab** ergänzt die Kommandozeile Ordner- und Dateinamen automatisch. Tippe `cd he` und drücke Tab -- daraus wird `cd help`.

---

## Ordnerinhalt anzeigen

| Befehl | Beschreibung |
|--------|-------------|
| `ls` | Dateien und Ordner auflisten (**l**i**s**t) |
| `ls help` | Inhalt eines bestimmten Ordners |
| `ls -la` (Mac) / `ls -Force` (Win) | Auch versteckte Dateien anzeigen |

```
cd ~/aipm
ls
# help/  leihsdir/  setup-guide.md  ...

ls help
# claudecode-basics.md  markdown-basics.md  obsidian-basics.md  ...

ls leihsdir
# leihsdir-context.md
```

> **Hinweis:** Dateien und Ordner, die mit einem Punkt beginnen (z.B. `.git`), sind standardmäßig versteckt. Mit `ls -la` (Mac) bzw. `ls -Force` (Windows) werden sie sichtbar.

---

## Dateien lesen

| Befehl | Beschreibung |
|--------|-------------|
| `cat Datei` | Gesamten Dateiinhalt anzeigen (con**cat**enate) |

```
cd ~/aipm
cat help/markdown-basics.md
# Zeigt den gesamten Inhalt der Datei
```

> **Tipp:** Bei langen Dateien scrollt der Inhalt schnell durch. Du kannst danach einfach hochscrollen.

---

## Dateien und Ordner erstellen

| Befehl | Beschreibung |
|--------|-------------|
| `mkdir Name` | Neuen Ordner erstellen (**m**a**k**e **dir**ectory) |
| `touch Name` (Mac) / `New-Item Name` (Win) | Neue leere Datei erstellen |

```
cd ~/aipm
mkdir notizen
ls
# help/  leihsdir/  notizen/  setup-guide.md  ...

# Mac:
touch notizen/ideen.md

# Windows:
New-Item notizen/ideen.md
```

---

## Dateien und Ordner verschieben, kopieren, umbenennen

| Befehl | Beschreibung |
|--------|-------------|
| `cp Quelle Ziel` | Datei kopieren (**c**o**p**y) |
| `mv Quelle Ziel` | Datei verschieben oder umbenennen (**m**o**v**e) |

```
cd ~/aipm

# Datei kopieren
cp help/markdown-basics.md notizen/markdown-kopie.md

# Datei umbenennen
mv notizen/ideen.md notizen/meine-ideen.md

# Datei in anderen Ordner verschieben
mv notizen/meine-ideen.md help/meine-ideen.md
```

---

## Dateien und Ordner löschen

| Befehl | Beschreibung |
|--------|-------------|
| `rm Datei` | Datei löschen (**r**e**m**ove) |
| `rm -r Ordner` (Mac) / `rm -Recurse Ordner` (Win) | Ordner mit Inhalt löschen |

```
cd ~/aipm
rm notizen/markdown-kopie.md

# Ganzen Ordner löschen:
# Mac:
rm -r notizen

# Windows:
rm -Recurse notizen
```

> **Achtung:** Gelöschte Dateien landen nicht im Papierkorb. Sie sind sofort weg. Sei vorsichtig mit `rm`.

---

## Bildschirm aufräumen

| Befehl | Beschreibung |
|--------|-------------|
| `clear` (Mac) / `cls` (Win) | Bildschirm leeren (**cl**ear **s**creen) |

Nützlich, wenn der Bildschirm nach vielen Befehlen unübersichtlich wird.

---

## Ordner im Finder / Explorer öffnen

| Befehl | Beschreibung |
|--------|-------------|
| `open .` (Mac) / `explorer .` (Win) | Aktuellen Ordner im Dateibrowser öffnen |

```
cd ~/aipm
# Mac:
open .

# Windows:
explorer .
```

Der Punkt `.` steht für "aktueller Ordner".

---

## Befehle, die Claude Code häufig ausführt

Wenn Claude Code einen Terminal-Befehl ausführen will, siehst du eine Genehmigungsabfrage. Hier die Befehle, die dabei am häufigsten vorkommen -- damit du einschätzen kannst, was passiert.

### Suchen und Finden

| Befehl                  | Beschreibung                                                                                 |
| ----------------------- | -------------------------------------------------------------------------------------------- |
| `grep "Text" Datei`     | In Dateien nach Text suchen (**g**lobally search a **r**egular **e**xpression and **p**rint) |
| `grep -r "Text" Ordner` | Rekursiv in allen Dateien eines Ordners suchen                                               |
| `find . -name "*.md"`   | Dateien nach Name suchen (hier: alle `.md`-Dateien)                                          |

```
# Wo kommt das Wort "LeihsDir" vor?
grep -r "LeihsDir" ~/aipm
# leihsdir/leihsdir-context.md: ...

# Alle Markdown-Dateien im Ordner finden
find ~/aipm -name "*.md"
# ~/aipm/help/markdown-basics.md
# ~/aipm/help/obsidian-basics.md
# ...
```

### Teile von Dateien lesen

| Befehl | Beschreibung |
|--------|-------------|
| `head -20 Datei` | Die ersten 20 Zeilen anzeigen |
| `tail -10 Datei` | Die letzten 10 Zeilen anzeigen |
| `wc -l Datei` | Zeilen zählen (**w**ord **c**ount) |

```
head -5 ~/aipm/help/markdown-basics.md
# Zeigt nur die ersten 5 Zeilen

wc -l ~/aipm/help/markdown-basics.md
# 129 help/markdown-basics.md
```

### Text in Dateien schreiben

| Befehl | Beschreibung |
|--------|-------------|
| `echo "Text" > Datei` | Text in Datei schreiben (überschreibt!) |
| `echo "Text" >> Datei` | Text an Datei anhängen |
| `sed 's/alt/neu/g' Datei` | Text ersetzen (**s**tream **ed**itor) |

> **Wichtig:** Ein `>` überschreibt die Datei komplett. Zwei `>>` hängen an. Achte auf den Unterschied.

### Git-Befehle

Claude Code nutzt Git, um den Zustand deiner Dateien zu verstehen.

| Befehl | Beschreibung |
|--------|-------------|
| `git status` | Zeigt geänderte/neue Dateien |
| `git diff` | Zeigt, was sich konkret geändert hat |
| `git log` | Zeigt die letzten Änderungen (Commits) |
| `git add Datei` | Datei für den nächsten Commit vormerken |
| `git commit -m "Text"` | Änderungen speichern mit Beschreibung |

> **Tipp:** Du musst Git nicht selbst beherrschen. Es reicht zu wissen, dass diese Befehle nur lesend sind (`status`, `diff`, `log`) oder Änderungen speichern (`add`, `commit`). Claude erklärt dir, was es vorhat.

---

## Zusammenfassung

Die 6 Befehle, die du am häufigsten brauchst:

| Befehl | Was er tut |
|--------|-----------|
| `cd` | In den Arbeitsordner wechseln (**c**hange **d**irectory) |
| `ls` | Schauen, was da ist (**l**i**s**t) |
| `pwd` | Prüfen, wo du bist (**p**rint **w**orking **d**irectory) |
| `cat` | Dateiinhalt lesen (con**cat**enate) |
| `mkdir` | Ordner anlegen (**m**a**k**e **dir**ectory) |
| `mv` | Datei verschieben/umbenennen (**m**o**v**e) |

> **Wenn etwas nicht klappt:** Prüfe mit `pwd`, ob du im richtigen Ordner bist. Das ist die häufigste Fehlerquelle.
