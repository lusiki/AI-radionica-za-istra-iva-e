# CLAUDE.md — Project Constitution

> This file is the "constitution" Claude reads at the start of every session.
> It is deliberately **slim** — the same design rule the harness teaches:
> Claude reliably follows ~100–150 instructions, so keep standing rules short and
> push detail into files that load only when relevant. (Aim ≤ ~120 lines.)

## What this project is
A presentation **and** follow-up resources that teach a group of **non-technical
methodological researchers** to move from *chat-prompting* to *agentic AI work*,
using an agentic Claude Code harness as the conceptual spine.

This repo is also, on purpose, a **tiny working example** of that harness — so the
medium demonstrates the message.

## Core principles
1. **Plan before building** anything non-trivial. Show me the plan; I approve before you edit files.
2. **Verify before declaring done.** Actually render / run the thing. Never claim success from imagination.
3. **Audience first.** They are non-technical methodologists. Frame agentic AI as *delegation,
   supervision, and reproducibility* — never as a "faster chatbot." Lead with their values:
   rigor, transparency, human judgment, integrity. Show failure modes + guardrails, not magic.
4. **Specialists beat a generalist;** a critic that cannot edit + a fixer that cannot bless
   its own work keeps the work honest.
5. **Write decisions to disk,** not just into the chat (plans, session notes) — chat gets wiped.

## Folder structure
The root reads as three tiers — **STROJ** (the machine/harness) · **RADIONICA** (content) · **IZVEDENO** (derived):
- `00-KRENI-OVDJE.md` — START-HERE map: walks the five harness layers and points at their real paths
- *STROJ:* `CLAUDE.md` + `.claude/` (the mini-harness: `skills/`, `rules/`, `agents/`, `constitutional-governance.md`); `pregled.html` is the clickable door into `.claude/` (open locally)
- *RADIONICA — web docs (stay at root; URLs frozen):* `index.qmd` → `docs/index.html`; `primjeri.qmd` / `setup.qmd` / `vjezba.qmd`; `slides/` is the RevealJS deck (`talk.qmd`), the dog-food artifact
- *RADIONICA — content (`radionica/`, Croatian, numbered for reading order):*
  - `00-razumijevanje/mapa-okvira.md` — annotated study map of the full harness (for Luka)
  - `01-postavljanje/README.md` — interfaces, prerequisites & pricing (included by `setup.qmd`)
  - `02-primjeri/README.md` — empirical example: clone from GitHub + two worked examples
  - `03-komplet/` — takeaway kit: `README.md` (plan) + `pojmovnik.md` (glossary)
- *IZVEDENO (never hand-edited):* `docs/` — build output served by GitHub Pages (main /docs); `quality_reports/` — working memory (plans, reviews)

## Skills (the buttons)
| Command      | What it does                                                        |
|--------------|---------------------------------------------------------------------|
| `/render`    | Build `slides/talk.qmd` to HTML and verify it actually rendered     |
| `/proofread` | Grammar / consistency / overflow pass on the slides before sharing  |
| `/commit`    | Stage + commit with a clear message — only after I say so           |
| `/review-deck` | Adversarial critic→fixer loop on the deck, then a 0–100 score      |

## Rules (handbooks — auto-load by relevance)
- `.claude/rules/plan-first-workflow.md` — **always-on**: plan before building.
- `.claude/rules/verification-protocol.md` — *on `.qmd`*: render before "done".
- `.claude/rules/quality-gates.md` — *on slides/resources*: the 80/90/95 score.
- `.claude/rules/audience-framing.md` — *on slides/resources*: how to pitch to methodologists.

## Agents (the crew — called by skills, not by you)
- `deck-critic` — read-only fault-finder + scorer (cannot edit).
- `deck-fixer` — read-write repairer (cannot approve its own work).
- `audience-reviewer` — read-only framing specialist.

## Governance
`.claude/constitutional-governance.md` holds the higher-altitude Articles (Plan-First, Quality Gate,
Verification, Adversarial Review, Memory, Audience Fidelity). They override this file on conflict.

## Current state (2026-06-22)
- Building blocks present: **constitution** (this file), **rules** (4), **governance**, **skills** (4),
  **agents** (3). The one layer not yet built is **settings + hooks** (layer 5) — add when ready.
- **Repo reorg (branch `repo-reorg-two-world`):** root regrouped into three tiers (STROJ / RADIONICA / IZVEDENO);
  content moved under `radionica/00–03`; `00-KRENI-OVDJE.md` added; web-doc `.qmd` + `slides/` kept at root so URLs + QR stay frozen.
- **Language:** audience-facing content + the study map are in **Croatian** (`slides/talk.qmd`,
  `radionica/`); the machinery (this file, rules, agents, governance) stays English.
  English block/skill/agent names are kept and bracketed as *hrvatski pojam (english-name)*; slash-commands stay English.
- **HTML overview:** `pregled.html` — a clickable index of every building block; each name links to the file.
- **Published web page:** `index.qmd` → `docs/index.html`, live at https://lusiki.github.io/AI-radionica-za-istra-iva-e/ (GitHub Pages, source main /docs).
- **Web docs:** `primjeri.qmd` (examples + clickable tiles), `setup.qmd` (interfaces/prereqs/prices), `vjezba.qmd` (guided exercise) → `docs/*.html`. The presentation links to these via tiles.
- **Onboarding:** `radionica/01-postavljanje/` (interfaces + prereqs + pricing) and `radionica/02-primjeri/` (clone-and-run empirical example), both Croatian.
- **Quarto installed** (1.9.x) — `quarto render` builds the deck + document into `docs/`.
- Resources: Croatian glossary at `radionica/03-komplet/pojmovnik.md`, quality-gate card + cheat sheet still to build.
- **Git:** connected to GitHub `origin` → `lusiki/AI-radionica-za-istra-iva-e` (branch `main`).

## How we work
- Quality bar: do not ship a slide with a typo, an overflowing block, or an unverifiable claim.
- Use the **same word for the same concept** across every slide and handout (e.g. always "task spec").
- I commit nothing until I say so out loud. Never push unless asked.
