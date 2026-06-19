# The Sant'Anna Claude Code Harness — an annotated study map

Your reference for understanding the machine *behind* the executive map. The talk delivers the
**why**; this delivers the **how**, with exact files, mechanics, and the plain-English analogy for each.

Source: <https://psantanna.com/claude-code-my-workflow/workflow-guide.html> ·
template repo: `pedrohcgs/claude-code-my-workflow` (a single ~2.3 MB HTML guide + a forkable repo).

> **How to use this:** read it once top-to-bottom, then do the **guided exercise** at the bottom in
> *this* folder. You'll understand the harness far faster by feeling the loop once than by reading
> the whole guide.

---

## The whole thing in one breath

You describe what you want in plain English. Claude acts as a general contractor: it drafts a plan,
gets your approval, hires a crew of specialist sub-agents, inspects their work, sends them back to
fix what's wrong, and returns to you only when the job passes inspection. **You talk, Claude runs the
site.** Everything else is plumbing built so you never think about plumbing.

---

## The five layers (where each lives, what it does, the analogy)

All project config lives in a hidden `.claude/` directory plus a root `CLAUDE.md`.

### 1. `CLAUDE.md` — the Constitution
- **Where:** project root. Read at the **start of every session.**
- **Mechanics:** a *slim* page (~120 lines; **hard ceiling ~150**). The reason is a hard limit:
  *Claude reliably follows only ~100–150 instructions, and the system prompt already eats ~50.*
  `CLAUDE.md` **and** the always-on rules share that one budget. Past ~150 lines, "Claude starts
  ignoring rules silently." Everything detailed moves out into path-scoped rules.
- **Analogy:** a one-page syllabus. List 300 rules and students follow none.

### 2. Rules — the Handbooks
- **Where:** `.claude/rules/*.md`. Load **automatically**.
- **Mechanics:** the key trick is **path-scoping** via a `paths:` line in the file's frontmatter —
  e.g. `paths: ['**/*.R']` means the R handbook only appears when Claude touches an `.R` file.
  Inventory: **32 rules**, of which ~27 are path-scoped; only ~5 are "always-on" (no `paths:`).
- **Analogy:** a professor doesn't memorise every style guide; the right one appears on the desk when
  grading that kind of assignment, and disappears when it's not needed. That's how 32 rules never
  clutter the model's attention.

### 3. Skills — the Buttons
- **Where:** `.claude/skills/<name>/SKILL.md` (one folder per skill).
- **Mechanics:** a `SKILL.md` is YAML frontmatter (`name`, `description`, `argument-hint`) + numbered
  steps. Invoked two ways: **explicitly** (you type `/proofread`) or **automatically** (Claude reads
  your plain-English request and picks the right skill). Inventory: **52 skills.**
- **Analogy:** named recipes. You rarely press the button yourself — you name the goal and Claude
  presses the right one.

### 4. Agents — the Crew
- **Where:** `.claude/agents/<name>.md`. **Called by skills, never by you directly.**
- **Mechanics:** each agent is a narrow specialist (grammar; layout/overflow; R code; domain
  substance; …). Frontmatter pins `model`, `effort`, `maxTurns` (runaway guard), `tools`/
  `disallowedTools` (e.g. a **read-only** critic), `permissionMode`. Inventory: **18 agents.**
  An orchestrator skill fans them out **in parallel**, then synthesises.
- **Analogy:** the specialist staff the manager assigns. *"A single prompt checking grammar, layout,
  math, and code at once does a mediocre job at all of them."*

### 5. Settings + Hooks — the Automatic Systems
- **Where:** `.claude/settings.json` (permissions + hooks) and `.claude/hooks/*.py`.
- **Mechanics:** **permissions** decide what Claude may do unattended. **Hooks** fire on events
  (Stop, PreCompact, PostToolUse, …). Inventory: **7 hooks** (session logging, desktop notify,
  context-survival, a context monitor warning at 40/55/65/80/90%, **git guardrails** that physically
  block `git reset --hard` / `push --force`, a stale-number reconciler) + a real git pre-commit hook.
- **Analogy:** a building's smoke alarm. Key insight: *"Rules live in context and can be compressed
  away. Hooks live in settings.json and fire **every time**, regardless of context state."* So
  enforcement that must survive a long session is a **hook**, not an instruction.

---

## The two ideas that make it work

1. **Specialists beat a generalist.** (Layer 4 above.)
2. **The adversarial loop** (the heart). A **critic** (read-only — *cannot* edit) lists every fault;
   a **fixer** (read-write) repairs them; the critic re-audits. Repeat until a round finds nothing
   new ("**loop-until-dry**": converge after 2 dry rounds; 5-round cap as a fallback).
   - *Why it works:* "The critic can't fix files, so it has no incentive to downplay issues. The
     fixer can't approve itself." → kills the "looks good" failure. **It's peer review.**

## The two rules that keep it honest

- **The 80 / 90 / 95 gate.** Every file scored 0–100. **80** = safe to commit; **90** = ready to
  ship (PR); **95** = excellence; **below 80 = blocked.** Sample deductions: equation overflow −20,
  broken citation −15, equation typo −10. A git pre-commit hook can enforce ≥80 on every commit.
- **The verification rule.** Claude may not say "done" until it has actually compiled / rendered /
  run the output. (This is why our `/render` skill *checks the HTML exists* before reporting success.)

---

## Memory — the four drawers (+ why)

Long sessions get **auto-compacted** (lossy: it keeps recent turns, drops the middle). The live chat
is the one thing that doesn't survive. So everything worth keeping goes to **disk**:

| Drawer | File / dir | Holds | Updated |
|---|---|---|---|
| Constitution | `CLAUDE.md` | standing rules | rarely |
| Corrections log | `MEMORY.md` | lessons, via a `[LEARN]` tag, so a mistake isn't repeated | on learning |
| Plans | `quality_reports/plans/` | strategy for the current task | once per task |
| Session logs | `quality_reports/session_logs/` | the **why** behind each choice | incrementally |

*"Git records **what**; session logs record **why**."* Paired hooks (`PreCompact` →
`SessionStart`) stash a note just before memory is wiped and read it back when the next session opens.

## How a real job flows

**Plan-first** (read-only; Claude drafts a plan, saves it, you approve) **→ Contractor mode**
(autonomous): IMPLEMENT → VERIFY → REVIEW (parallel specialist agents) → FIX (worst-first) →
RE-VERIFY → SCORE → converged? loop or present summary. *It commits nothing until you say so.*
Note: the orchestrator is **"a runtime, not a daemon"** — nothing fires it on its own; plan approval
does **not** auto-start it. The human is the auditor of the disagreements the loop surfaces.

## Cost — the 70 / 20 / 10 staffing pattern

Per-agent model routing, set with a `model:` line in each agent file:

- **Haiku (fast/cheap) ≈ 70%** — mechanical (extraction, reformatting, validation, proofread fixes)
- **Sonnet (mid) ≈ 20%** — review/critique
- **Opus (top) ≈ 10%** — high-judgment (editor, referees, claim verification)

Savings vs. all-Opus: **50–80%**, no quality loss on the mechanical tier. A second dial is **effort**
(`low → medium → high → xhigh → max`); "Haiku + high effort" can beat "Opus + low effort" on bounded
tasks. Monitor with `/cost` and `/usage`.

## Getting started (the real template, when you're ready)

Three things: **install Claude Code → fork `pedrohcgs/claude-code-my-workflow` → paste one starter
prompt** naming your project. Claude reads the config, fills in your details, proposes
customisations, shows a plan, you approve. Then *"start with just `CLAUDE.md` and 2–3 skills, add the
rest as you discover what you need"* — **the ceiling, not the floor.**

---

## How *this* folder maps to the full harness

You're already standing in a (deliberately tiny) instance of it:

| Full harness | In this repo | Note |
|---|---|---|
| Constitution | [`../CLAUDE.md`](../CLAUDE.md) | slim, ~1 page — exactly the design rule |
| Rules (handbooks) | `../.claude/rules/` (4 files) | 1 always-on + 3 path-scoped — demonstrates the `paths:` trick |
| Constitutional governance | [`../.claude/constitutional-governance.md`](../.claude/constitutional-governance.md) | Articles I–VI (normally optional / added later) |
| Skills (buttons) | `../.claude/skills/{render,proofread,commit,review-deck}/` | `/review-deck` is the orchestrator |
| Agents (crew) | `../.claude/agents/{deck-critic,deck-fixer,audience-reviewer}.md` | read-only critic + read-write fixer + a specialist |
| Adversarial loop | `/review-deck` wires critic → fixer → re-audit | the heart, in miniature |
| Specialists-beat-generalist | `/proofread` (4 passes) + 2 distinct review agents | grammar / consistency / overflow / claims / framing |
| Verification rule | `/render` checks the `.html` exists | "don't claim done without checking" |
| Quality gate | `../.claude/rules/quality-gates.md` | the 80 / 90 / 95 score |
| Model tiers (70/20/10) | `model:` in each agent file | critic = sonnet, fixer = haiku, reviewer = sonnet |
| Memory drawers | `~/.claude/.../memory/` | already recording this project |
| Settings + hooks | *(not built yet — layer 5)* | the one remaining block; offered next |

## Guided exercise — run the loop once (≈ 20 min)

1. **Install Quarto** (`winget install --id Posit.Quarto -e`, then reopen the shell).
2. Ask Claude, in plain English: *"Add a closing 'thank you / questions' slide to the deck, then
   render it."* — watch it **plan first**.
3. **Approve the plan.** Watch contractor mode: it edits `talk.qmd`, runs `/render`, and **verifies**
   the HTML built before saying done.
4. Run `/proofread slides/talk.qmd` and read the severity-grouped findings.
5. Run `/commit` — watch it **ask before** `git init` and **before** committing. *You* stay in control.

That round — plan → act → verify → review → your approval — *is* the whole harness in miniature.
