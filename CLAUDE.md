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
- `index.qmd`     — the talk as a Quarto HTML document → renders to `docs/` (published via GitHub Pages)
- `pregled.html`  — clickable building-block overview (open locally)
- `slides/`       — the Quarto → RevealJS deck (`talk.qmd`), the dog-food artifact
- `resources/`    — the takeaway kit (glossary, quality-gate card, cheat sheet)
- `setup/`       — interfaces, prerequisites & pricing (Croatian)
- `demos/`        — empirical example: clone from GitHub + two worked examples (Croatian)
- `harness-map/`  — my annotated study map of the full harness (for Luka)
- `.claude/`      — this mini-harness: `skills/`, `rules/`, `agents/`, `constitutional-governance.md`

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

## Current state (2026-06-19)
- Building blocks present: **constitution** (this file), **rules** (4), **governance**, **skills** (4),
  **agents** (3). The one layer not yet built is **settings + hooks** (layer 5) — add when ready.
- **Language:** audience-facing content + the study map are in **Croatian** (`slides/talk.qmd`,
  `resources/`, `harness-map/`); the machinery (this file, rules, agents, governance) stays English.
  English block/skill/agent names are kept and bracketed as *hrvatski pojam (english-name)*; slash-commands stay English.
- **HTML overview:** `pregled.html` — a clickable index of every building block; each name links to the file.
- **Published web page:** `index.qmd` → `docs/index.html`, live at https://lusiki.github.io/AI-radionica-za-istra-iva-e/ (GitHub Pages, source main /docs).
- **Onboarding:** `setup/` (interfaces + prereqs + pricing) and `demos/` (clone-and-run empirical example), both Croatian.
- **Quarto installed** (1.9.x) — `quarto render` builds the deck + document into `docs/`.
- Resources: Croatian glossary in `resources/`, quality-gate card + cheat sheet still to build.
- **Git:** connected to GitHub `origin` → `lusiki/AI-radionica-za-istra-iva-e` (branch `main`).

## How we work
- Quality bar: do not ship a slide with a typo, an overflowing block, or an unverifiable claim.
- Use the **same word for the same concept** across every slide and handout (e.g. always "task spec").
- I commit nothing until I say so out loud. Never push unless asked.
