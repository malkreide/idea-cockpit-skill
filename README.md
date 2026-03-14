# idea-cockpit-skill

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Claude Skill](https://img.shields.io/badge/claude-skill-orange)

> A Claude skill that turns Claude into a structured idea manager using the Idea Flight Deck framework with direct Notion integration.

[🇩🇪 Deutsche Version](README.de.md)

---

## Overview

The **Idea Cockpit Skill** implements the «Idea Flight Deck» framework — a lightweight,
opinionated system for managing ideas through a maturity model directly in Notion.

Instead of a chaotic notes pile, every idea moves through defined stages: from a raw
**Spark** (🌱) to a **Concept** (🧩), a **Plan** (🗺️), to **Active** (🚀) — with a
hard limit of 3 active ideas at any time. Ideas that aren't ready yet are deliberately
**Frozen** (❄️) rather than deleted.

Claude handles the capture, triage, and weekly ritual — you stay focused on the work.

---

## Features

- **Fast capture** — New idea in Notion in under 30 seconds, with only 2 questions
- **Maturity model** — 5 stages from raw spark to active project
- **3-Active limit** — Enforces focus; promotes before adding new active items
- **Weekly Ritual** — Structured 15-minute Monday routine to triage and advance ideas
- **Quarterly Review** — Pattern recognition on long-dormant sparks
- **Direct Notion integration** — No copy-paste; Claude writes directly to your database
- **Anti-elaboration principle** — Capture first, develop later

---

## Prerequisites

- [Claude.ai](https://claude.ai) account (Pro recommended for project skills)
- A Notion account with API access
- Notion MCP server connected to Claude ([setup guide](https://mcp.notion.com))
- A Notion database with the schema described below

---

## Installation

### Step 1: Set up your Notion database

Create a new Notion database (or duplicate the template — see below) with these properties:

| Property | Type | Options |
|---|---|---|
| Title | Title | — |
| Maturity | Select | 🌱 Spark, 🧩 Concept, 🗺️ Plan, 🚀 Active, ❄️ Frozen |
| Next Step | Rich Text | — |
| Area | Select | Your work areas (e.g. Work, Personal) |
| Energy | Select | ⚡ High, 🔋 Medium, 🪫 Low |
| Notes | Rich Text | — |

### Step 2: Get your Notion IDs

1. Open your Notion database in the browser
2. Copy the database ID from the URL:  
   `https://www.notion.so/**5ca924784c654d0b84a2cc1ed6c127c0**`
3. Get your Data Source ID via the Notion MCP tool (use `notion-fetch` on the database URL)

### Step 3: Configure SKILL.md

Open `SKILL.md` and replace the placeholders in the **Notion Configuration** section:

```yaml
Database ID:    YOUR_DATABASE_ID      → your actual database ID
Data Source ID: YOUR_DATA_SOURCE_ID   → your actual data source ID
```

### Step 4: Upload to Claude

1. Open your Claude.ai project
2. Go to **Project Settings → Files**
3. Upload the configured `SKILL.md`
4. The skill activates automatically based on trigger patterns

---

## Usage / Quickstart

Once the skill is active, just speak naturally:

```
"I have a new idea: ..."
"Let's do the Weekly Ritual"
"What am I currently working on?"
"Freeze the GitHub Automation idea"
"What ideas have I been ignoring?"
```

Claude will ask the minimal necessary questions and write directly to Notion.

---

## The Maturity Model

```
🌱 Spark      Raw flash of thought. No Next Step required.
    ↓
🧩 Concept    Problem and solution direction are clear. Next Step defined.
    ↓
🗺️ Plan       Next 3 steps mapped out.
    ↓
🚀 Active     In progress. Has a deadline. MAX 3 AT A TIME.
    
❄️ Frozen     Deliberately paused. Date and reason noted.
```

---

## Project Structure

```
idea-cockpit-skill/
├── SKILL.md        ← The skill (configure your Notion IDs here)
├── README.md       ← This file
├── README.de.md    ← German documentation
├── LICENSE         ← MIT License
└── CHANGELOG.md    ← Version history
```

---

## Workflow Overview

| Workflow | Trigger | Duration |
|---|---|---|
| Capture new idea | «I have an idea: ...» | ~30 seconds |
| Weekly Ritual | «Let's do the Weekly» | ~15 minutes |
| Promote/Freeze idea | «Freeze X» / «Move X to Active» | ~1 minute |
| Quarterly Review | Manual trigger | ~30 minutes |

---

## Changelog

See [CHANGELOG.md](CHANGELOG.md)

---

## License

MIT License — see [LICENSE](LICENSE)

---

## Author

**Hayal Oezkan** · [@malkreide](https://github.com/malkreide)  

---

## Acknowledgements

Inspired by:
- Tiago Forte's *Building a Second Brain* (PARA method)
- GTD (Getting Things Done) by David Allen
- The concept of deliberate idea maturation over impulsive execution

---

*Made with ❤️ in Zürich*
