---
description: Never declare a slide task done without actually rendering it.
paths: ['**/*.qmd', 'slides/**']
---

# Verification Protocol  (loads when working on slides)

You may **not** report a deck task as "done" until you have actually rendered it and confirmed the
output exists.

- After any edit to a `.qmd`, run `/render` (which runs `quarto render` and checks the `.html` exists).
- If the render fails, read the error, fix the source, and re-render. Loop until it builds clean.
- If Quarto is not installed, say so plainly and STOP — do not claim success from imagination.

"Done" means *rendered and verified*, never *looks right in my head*.
