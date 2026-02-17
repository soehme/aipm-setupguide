# Das @-Zeichen in Claude Code

## Wozu dient @?

Mit dem `@`-Zeichen kannst du Claude Code gezielt auf bestimmte Dateien oder Ordner hinweisen. So weiss Claude genau, womit es arbeiten soll.

Beispiel:
```
Les @leihsdir/leihsdir-context.md und fasse den Inhalt zusammen.
Vergleiche @help/markdown-basics.md mit @help/obsidian-basics.md.
```

Leider gibt es noch einen Bug im Terminal-Plugin, der das Tippen des @-Zeichens unter MacOS verhindert.

Der Bugfix ist schon fast verfügbar ([PR #92](https://github.com/polyipseity/obsidian-terminal/pull/92))

Bis dahin ist unser Workaround: Copy&Paste.

Hier die Vorlage:

```md
@
```