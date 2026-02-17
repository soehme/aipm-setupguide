# Markdown Basics

Markdown ist eine einfache Auszeichnungssprache, mit der du Text formatieren kannst. Du schreibst normalen Text und fügst ein paar Sonderzeichen hinzu -- den Rest erledigt der Editor.

Hier die wichtigsten Auszeichnungen einmal roh (wie du sie schreibst) und darunter wie sie dir dann angezeigt werden

## Überschriften

```markdown
# Überschrift 1 (größte)
## Überschrift 2
### Überschrift 3
```

# Überschrift 1 (größte)
## Überschrift 2
### Überschrift 3


## Textformatierung

```markdown
**fett**
*kursiv*
~~durchgestrichen~~
`Code inline`
```

**fett**, *kursiv*, ~~durchgestrichen~~, `Code inline`

## Listen

**Aufzählung:**
```markdown
- Punkt 1
- Punkt 2
  - Unterpunkt
```

- Punkt 1
- Punkt 2
	- Unterpunkt

**Nummeriert:**
```markdown
1. Erster Punkt
2. Zweiter Punkt
3. Dritter Punkt
```

1. Erster Punkt
2. Zweiter Punkt
3. Dritter Punkt

## Links und Bilder

```markdown
[[setup-guide]]
[Link-Text](https://example.com)
![Bild-Beschreibung](bild.png)
```

[[setup-guide]]
[codecentric AG](https://www.codecentric.de)
![Unser Logo](https://www.codecentric.de/_next/image?url=https%3A%2F%2Feu-central-1.graphassets.com%2FAiE4QoWSSiIQO3k152ugkz%2Foutput%3Dformat%3Awebp%2FK1lI4UPCSUuKSWZHgd4D&w=640&q=75)


## Codeblöcke

Drei Backticks für mehrzeiligen Code:

````markdown
```python
print("Hallo Welt")
```
````

```python
print("Hallo Welt")
```


## Zitate

```markdown
> Das ist ein Zitat.
> Es kann mehrere Zeilen haben.
```

> Das ist ein Zitat.
> Es kann mehrere Zeilen haben.

## Tabellen

```markdown
| Spalte 1 | Spalte 2 |
|----------|----------|
| Wert A   | Wert B   |
| Wert C   | Wert D   |
```

| Spalte 1 | Spalte 2 |
|----------|----------|
| Wert A   | Wert B   |
| Wert C   | Wert D   |

## Horizontale Linie

```markdown
---
```


---

## Checklisten

```markdown
- [ ] Aufgabe offen
- [x] Aufgabe erledigt
```

- [ ] Aufgabe offen
- [x] Aufgabe erledigt

---

**Tipp:** Du musst dir nicht alles merken. Schreib einfach los -- die wichtigsten Formatierungen (`#`, `**`, `-`) decken 90% der Fälle ab.
