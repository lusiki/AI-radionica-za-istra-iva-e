---
name: commit
description: Stage and commit changes with a clear message — only after the user explicitly approves. Use when the user says to commit / save progress.
argument-hint: "[short description of the change]"
---

# Steps

1. If this folder is **not** a git repo yet, **ask the user before** running `git init`
   (note: it lives inside a Dropbox folder, so mention that git + Dropbox can occasionally
   double-sync — usually fine for a small project).
2. Show `git status` and `git diff --stat` so the user can see exactly what changed.
3. Propose a one-line commit message describing **what** changed and **why**.
4. Only after the user says go: `git add` the relevant files and commit.
   **Never** commit without explicit approval.
5. Do **not** push unless the user asks.
