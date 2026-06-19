---
name: proofread
description: Proofread the slides as separate specialist passes (grammar, terminology consistency, overflow, unverifiable claims) before sharing. Use before showing or committing the deck.
argument-hint: "[path to .qmd — defaults to slides/talk.qmd]"
---

# Steps

1. Read the target `.qmd` (default `slides/talk.qmd`).
2. Run **four separate passes** — specialists beat a generalist; one combined pass misses things:
   - **(a) Grammar / typos.**
   - **(b) Terminology consistency** — the same word for the same concept on every slide
     (e.g. always "task spec", never silently switch to "prompt" or "instructions").
   - **(c) Overflow / density** — flag slides with more than ~6 bullets, long code blocks, or
     anything likely to run off the slide in RevealJS.
   - **(d) Unverifiable / risky claims** — numbers, citations, or strong assertions that should be
     checked before an academic audience sees them.
3. Present findings grouped by severity: **Critical / Major / Minor**. Do **not** edit yet — list them.
4. After the user approves fixes, apply them, then invoke `/render` to confirm the deck still builds.
