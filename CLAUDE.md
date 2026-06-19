# CLAUDE.md — Project Constitution

> This file is the "constitution" Claude reads at the start of every session.
> It is deliberately **slim** — the same design rule the Sant'Anna harness teaches:
> Claude reliably follows ~100–150 instructions, so keep standing rules short and
> push detail into files that load only when relevant. (Aim ≤ ~120 lines.)

## What this project is
A presentation **and** follow-up resources that teach a group of **non-technical
methodological researchers** to move from *chat-prompting* to *agentic AI work*,
using the Sant'Anna Claude Code harness as the conceptual spine.

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
- `slides/`       — the Quarto → RevealJS deck (`talk.qmd`), the dog-food artifact
- `resources/`    — the takeaway kit (glossary, quality-gate card, cheat sheet)
- `demos/`        — scripted demo steps + recorded fallbacks (for later)
- `harness-map/`  — my annotated study map of the full Sant'Anna harness (for Luka)
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
- **Quarto not yet installed** — `/render` will stop and tell you to install it. See `harness-map/README.md`.
- Resources: Croatian glossary in `resources/`, quality-gate card + cheat sheet still to build.
- **Git:** connected to GitHub `origin` → `lusiki/AI-radionica-za-istra-iva-e` (branch `main`).

## How we work
- Quality bar: do not ship a slide with a typo, an overflowing block, or an unverifiable claim.
- Use the **same word for the same concept** across every slide and handout (e.g. always "task spec").
- I commit nothing until I say so out loud. Never push unless asked.
