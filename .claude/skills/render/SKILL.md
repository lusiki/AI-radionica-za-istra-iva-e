---
name: render
description: Render the Quarto RevealJS deck to HTML and verify it actually built. Use when asked to render/build/preview the slides or check that the deck still compiles.
argument-hint: "[path to .qmd — defaults to slides/talk.qmd]"
---

# Steps

1. **Resolve target.** Use the argument if given, otherwise `slides/talk.qmd`.
2. **Check the tool exists.** Run `quarto --version`. If Quarto is missing, **STOP** and tell the
   user to install it (`winget install --id Posit.Quarto -e`, then restart the shell). Do **not**
   pretend the render succeeded — that violates the verification rule this project teaches.
3. **Render.** Run `quarto render <target>`.
4. **VERIFY (mandatory).** Confirm the command exited 0 **and** the output `.html` exists. Report
   its path. You may not say "done" without this check.
5. **If it failed,** read the error, fix the `.qmd`, and re-render. Loop until it builds clean.
6. Offer to open it: `quarto preview <target>` (live-reload) for working on the deck.
