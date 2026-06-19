---
name: review-deck
description: Adversarial review-fix loop on the talk deck — fan out read-only specialist reviewers, apply fixes with the fixer, re-audit in fresh context, loop until clean, then score. Use when asked to review/critique/polish the deck or check it's ready to present.
argument-hint: "[path to .qmd — defaults to slides/talk.qmd]"
---

# Steps  (this is the orchestrator / adversarial loop, in miniature)

1. **VERIFY first.** Run `/render` on the target. If it won't build, fix that before reviewing.
2. **REVIEW (fan out, read-only, in parallel).** Spawn two specialists as subagents:
   - `deck-critic` — substance, clarity, consistency, overflow; assigns severity + a 0–100 score.
   - `audience-reviewer` — checks the non-technical-methodologist framing (delegation not
     productivity, values-first, failure+guardrails, consistent vocabulary).
   Collect their findings, deduped, grouped **Critical / Major / Minor**.
3. **Converged?** If a round produced **0 new Critical/Major** findings, go to step 6.
4. **FIX.** Spawn `deck-fixer` (read-write) to apply the findings **worst-first**. The fixer does not
   score or approve — it only repairs.
5. **RE-VERIFY + RE-REVIEW** in fresh context: `/render`, then re-run `deck-critic`. Loop to step 3.
   (Converge after **2 dry rounds**; hard cap **5 rounds**.)
6. **SCORE** via `.claude/rules/quality-gates.md` and present a short summary: score, what changed,
   what (if anything) is still open. **Commit nothing** — wait for the human.
