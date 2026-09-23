# Troubleshooting (Claude Code)

Probleme, die nur Claude Code betreffen. Alles rund um git, Node.js, Obsidian-Einstellungen und das Terminal-Plugin steht in [troubleshooting.md](../troubleshooting.md) eine Ebene höher.

---

## Plan B: Claudian statt Terminal-Plugin

Wenn das Terminal-Plugin nicht zuverlässig läuft -- das passiert vor allem unter Windows --, ist Claudian eine Alternative: ein Obsidian-Plugin, das deinen KI-Assistenten direkt als Chat-Fenster in Obsidian einbettet, ohne Terminal.

**1. Claudian installieren:**

1. Einstellungen -> Community Plugins -> **"Browse"**
2. Nach **"Claudian"** suchen
3. Achte auf den Autor **Yishen Tu** -- es gibt mehrere ähnlich benannte Abwandlungen von anderen Autoren
4. **"Install"** und dann **"Enable"** klicken

**2. Claudian einrichten:**

1. Öffne die Claudian-Einstellungen (Community Plugins -> Claudian -> Zahnrad-Symbol)
2. Wähle als Agent **Claude Code**
3. Scrolle ganz nach unten zu **"Advanced"** und aktiviere **"Enable bash mode (!)"**

**3. Claudian starten:**

1. Klicke auf das Roboter-Symbol in der linken Symbolleiste
2. Stelle oben im Chat-Fenster den Modus von **YOLO** auf **Safe** um
3. Wähle als Modell **Sonnet** und als Thinking-Stufe **Medium**

> **Warum Safe?** Im Safe-Modus fragt Claudian vor Dateiänderungen nach -- genau das wollen wir im Training sehen.
