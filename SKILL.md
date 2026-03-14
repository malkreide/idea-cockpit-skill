---
name: idea-cockpit
description: >
  Structured idea management using the «Idea Flight Deck» framework with direct
  Notion integration. Use this skill whenever the user wants to (1) capture and
  classify new ideas, (2) run the Weekly Ritual (triage sparks, promote or freeze
  ideas), (3) get an overview of active ideas, (4) doesn't know what to work on
  next, (5) feels overwhelmed or has lost track, (6) mentions terms like «Idea
  Cockpit», «Flight Deck», «Spark Inbox» or «maturity level», or (7) talks
  generally about idea management, Second Brain or personal knowledge management.
  Also use when the user says «I have too many ideas», «I'm losing track», or
  «I don't know where to start».
---

# Idea Cockpit Skill

This skill manages the «Idea Flight Deck» framework — a lightweight idea management
system that lives directly in Notion.

---

## Notion Configuration

> ⚠️ **Setup required:** Replace the placeholders below with your own Notion IDs.
> See [Installation](README.md#installation) for step-by-step instructions.

| Element | ID / URL |
|---|---|
| **Database ID** | `YOUR_DATABASE_ID` |
| **Data Source ID** | `YOUR_DATA_SOURCE_ID` |
| **Notion URL** | `https://www.notion.so/YOUR_DATABASE_ID` |

### Views
| View | Type | Purpose |
|---|---|---|
| 🗂️ Flight Deck (Kanban) | Board | Full overview by maturity level |
| 🚀 Active (max. 3) | Table | Ongoing ideas, filtered |
| 🌱 Spark Inbox | List | Raw ideas, chronological |
| ❄️ Frozen | Table | Deliberately paused ideas |

---

## Maturity Model

| Emoji | Status | Criterion |
|---|---|---|
| 🌱 | **Spark** | Raw idea, not yet evaluated — NO Next Step required |
| 🧩 | **Concept** | Problem + solution direction clear |
| 🗺️ | **Plan** | Next 3 steps defined |
| 🚀 | **Active** | In progress, deadline exists — max. 3 simultaneously |
| ❄️ | **Frozen** | Deliberately paused (note date in Notes field) |

---

## Database Schema

```
Title          TEXT (TITLE)
Maturity       SELECT: 🌱 Spark | 🧩 Concept | 🗺️ Plan | 🚀 Active | ❄️ Frozen
Next Step      RICH_TEXT  (required from maturity «Concept» onward)
Area           SELECT: Work | Personal | [your custom areas]
Energy         SELECT: ⚡ High | 🔋 Medium | 🪫 Low
Notes          RICH_TEXT
Created        CREATED_TIME
Last Moved     LAST_EDITED_TIME
```

---

## Workflows

### 1. Capture a New Idea

**Goal:** Fast, without elaboration. Under 30 seconds.

Steps:
1. Ask only two required questions: **«How clear is the idea?»** and **«Which area does it belong to?»** — via `ask_user_input_v0` (single_select per question)
2. Determine maturity based on clarity:
   - «Just a flash» → 🌱 Spark (no Next Step)
   - «Problem + direction clear» → 🧩 Concept (ask for Next Step)
   - «I know how to do it» → 🗺️ Plan (ask for Next Step + 3 sub-steps)
3. Enter directly into Notion via `notion-create-pages` with your `data_source_id`
4. Confirm with link to the database

**Important:** Never elaborate before the entry is in Notion. Capture first.

---

### 2. Weekly Ritual (Monday, ~15 min)

**Goal:** Gain overview, advance impulses, check capacity.

Steps:
1. Load current entries from Notion via `notion-search` in the database
2. **Review active ideas** (max. 3): Is the «Next Step» still current?
3. **Triage sparks**: Per spark, one question: «Relevant in the next 30 days?»
   - Yes + clear → 🧩 Concept, define Next Step
   - Yes + unclear → stays 🌱 Spark, optionally add note
   - No → delete or ❄️ freeze
4. **Promotions**: Suggest 1 idea from Spark → Concept (only if capacity available)
5. **Report**: Short summary — what's active, what's waiting, what was frozen

---

### 3. Promote or Freeze an Idea

When promoting:
- Next Step must be defined (otherwise stays at current maturity)
- When promoting to 🚀 Active: Check if 3 active ideas already exist → if yes, first freeze or close one

When freezing:
- Note date in Notes: «Frozen: [Month Year] — Reason: ...»
- Set maturity to ❄️

---

### 4. Quarterly Spark Review (4×/year, ~30 min)

All sparks that have been unchanged for >90 days:
- Still relevant? → keep
- Never looked at again? → archive (set maturity to ❄️, note «Archive»)

Identify patterns: Which themes keep coming up? Those are the real priorities.

---

## Interaction Principles

1. **Always enter directly** — never just display or suggest. Notion entry as the conclusion of every capture.
2. **Maximum 2 questions at once** — via `ask_user_input_v0`, never as prose list.
3. **Spark ≠ Concept** — never force a Next Step on a spark.
4. **Enforce the 3-Active limit** — if user wants to activate a 4th idea, first triage existing ones.
5. **No elaborating** — Claude does not develop an idea further unless the user explicitly asks. Capture, not coach.
6. **Use context** — adapt the Area options to the user's actual work contexts.

---

## Example Interactions

**Capture a new idea:**
> «I have an idea: AI-powered parent communication system for schools»
→ 2 Quick-Questions → Entry in Notion → Link

**Start Weekly:**
> «Let's do the Weekly» / «Can you help me triage my ideas?»
→ Load Notion → guide through all stages in a structured way

**Overview:**
> «What am I currently working on?» / «Show me my ideas»
→ Query Notion → clear response with maturity and Next Step

---

## Anti-Patterns (avoid)

- ❌ Elaborating an idea before it is captured
- ❌ Tolerating more than 3 Active simultaneously
- ❌ Requiring a Next Step for Sparks
- ❌ Running Weekly without querying Notion
- ❌ Deleting without user confirmation
