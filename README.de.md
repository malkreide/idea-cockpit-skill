[🇬🇧 English Version](README.md)

# idea-cockpit-skill

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Lizenz](https://img.shields.io/badge/lizenz-MIT-green)
![Claude Skill](https://img.shields.io/badge/claude-skill-orange)

> Ein Claude Skill, der Claude in einen strukturierten Ideen-Manager verwandelt — mit dem Idea Flight Deck Framework und direkter Notion-Integration.

---

## Übersicht

Der **Idea Cockpit Skill** implementiert das «Idea Flight Deck» Framework — ein schlankes, meinungsstarkes System, das Ideen über ein Reifegrad-Modell direkt in Notion verwaltet.

Statt eines chaotischen Notizhaufens durchläuft jede Idee definierte Stufen: vom rohen **Funken** (🌱) über ein **Konzept** (🧩) und einen **Plan** (🗺️) bis zu **Aktiv** (🚀) — mit einem harten Limit von 3 aktiven Ideen gleichzeitig. Ideen, die noch nicht reif sind, werden bewusst **eingefroren** (❄️) statt gelöscht.

Claude übernimmt die Erfassung, Triage und das Weekly Ritual — du bleibst fokussiert auf die eigentliche Arbeit.

---

## Funktionen

- **Schnelle Erfassung** — Neue Idee in Notion in unter 30 Sekunden, mit nur 2 Fragen
- **Reifegrad-Modell** — 5 Stufen vom rohen Funken bis zum aktiven Projekt
- **3-Aktiv-Limit** — Erzwingt Fokus; Beförderung erst nach Kapazitätsprüfung
- **Weekly Ritual** — Strukturierte 15-Minuten-Routine jeden Montag für Triage und Fortschritt
- **Quarterly Review** — Mustererkennung bei lang ruhenden Funken
- **Direkte Notion-Integration** — Kein Copy-Paste; Claude schreibt direkt in deine Datenbank
- **Anti-Ausarbeitungs-Prinzip** — Erst erfassen, dann entwickeln

---

## Voraussetzungen

- [Claude.ai](https://claude.ai) Account (Pro empfohlen für Projekt-Skills)
- Notion-Account mit API-Zugriff
- Notion MCP-Server mit Claude verbunden ([Setup-Anleitung](https://mcp.notion.com))
- Eine Notion-Datenbank mit dem unten beschriebenen Schema

---

## Installation

### Schritt 1: Notion-Datenbank einrichten

Erstelle eine neue Notion-Datenbank (oder dupliziere eine Vorlage) mit diesen Eigenschaften:

| Eigenschaft | Typ | Optionen |
|---|---|---|
| Titel | Title | — |
| Reifegrad | Select | 🌱 Funke, 🧩 Konzept, 🗺️ Plan, 🚀 Aktiv, ❄️ Eingefroren |
| Nächster Schritt | Rich Text | — |
| Bereich | Select | Deine Arbeitsbereiche (z.B. SAM, Persönlich) |
| Energie | Select | ⚡ Hoch, 🔋 Mittel, 🪫 Niedrig |
| Notizen | Rich Text | — |

### Schritt 2: Notion-IDs ermitteln

1. Öffne deine Notion-Datenbank im Browser
2. Kopiere die Datenbank-ID aus der URL:  
   `https://www.notion.so/**5ca924784c654d0b84a2cc1ed6c127c0**`
3. Ermittle deine Data Source ID über das Notion MCP-Tool (`notion-fetch` auf der Datenbank-URL)

### Schritt 3: SKILL.md konfigurieren

Öffne `SKILL.md` und ersetze die Platzhalter im Abschnitt **Notion Configuration**:

```yaml
Database ID:    YOUR_DATABASE_ID      → deine tatsächliche Datenbank-ID
Data Source ID: YOUR_DATA_SOURCE_ID   → deine tatsächliche Data Source ID
```

### Schritt 4: In Claude hochladen

1. Öffne dein Claude.ai-Projekt
2. Gehe zu **Projekteinstellungen → Dateien**
3. Lade die konfigurierte `SKILL.md` hoch
4. Der Skill aktiviert sich automatisch basierend auf Trigger-Mustern

---

## Verwendung / Schnellstart

Sobald der Skill aktiv ist, sprich einfach natürlich:

```
«Ich habe eine neue Idee: ...»
«Lass uns das Weekly machen»
«Was habe ich gerade aktiv?»
«Friere die Idee X ein»
«Welche Ideen habe ich schon lange nicht mehr angeschaut?»
```

Claude stellt die minimal notwendigen Fragen und schreibt direkt in Notion.

---

## Das Reifegrad-Modell

```
🌱 Funke        Roher Gedankenblitz. Kein Nächster Schritt nötig.
    ↓
🧩 Konzept      Problem und Lösungsrichtung sind klar. Nächster Schritt definiert.
    ↓
🗺️ Plan         Die nächsten 3 Schritte sind geplant.
    ↓
🚀 Aktiv        In Bearbeitung. Hat eine Deadline. MAX. 3 GLEICHZEITIG.
    
❄️ Eingefroren  Bewusst pausiert. Datum und Grund vermerkt.
```

---

## Projektstruktur

```
idea-cockpit-skill/
├── SKILL.md        ← Der Skill (hier Notion-IDs konfigurieren)
├── README.md       ← Englische Dokumentation
├── README.de.md    ← Diese Datei
├── LICENSE         ← MIT-Lizenz
└── CHANGELOG.md    ← Versionsverlauf
```

---

## Workflow-Übersicht

| Workflow | Trigger | Dauer |
|---|---|---|
| Neue Idee erfassen | «Ich habe eine Idee: ...» | ~30 Sekunden |
| Weekly Ritual | «Lass uns das Weekly machen» | ~15 Minuten |
| Idee befördern/einfrieren | «Einfrieren X» / «X auf Aktiv setzen» | ~1 Minute |
| Quarterly Review | Manueller Trigger | ~30 Minuten |

---

## Änderungsprotokoll

Siehe [CHANGELOG.md](CHANGELOG.md)

---

## Lizenz

MIT-Lizenz — siehe [LICENSE](LICENSE)

---

## Autor

**Hayal Oezkan** · [@malkreide](https://github.com/malkreide)  
Leiter Marketing & Kommunikation, Schulamt der Stadt Zürich  
Mitglied, KI-Fachgruppe Stadt Zürich

---

## Danksagungen

Inspiriert von:
- Tiago Fortes *Building a Second Brain* (PARA-Methode)
- GTD (Getting Things Done) von David Allen
- Der Idee der bewussten Ideenreifung statt impulsiver Umsetzung

---

*Mit ❤️ gemacht in Zürich*
