# Glossary — from chat words to agentic words

A one-page translation table for the audience. **Keep this wording identical** everywhere it appears
(slides, cheat sheet, repo) so it reinforces one mental model instead of fragmenting it.

| You say now (chat world) | The agentic word | So what — in plain language |
|---|---|---|
| Prompt | **Task spec** | The job description: the goal, the constraints, and what "done" looks like. Like a methods section, not a vague ask. |
| Conversation / thread | **Agent loop** | Perceive → decide → act → check → repeat, possibly many steps — not one question and one answer. |
| "Copy the code and run it yourself" | **Tool use** | The agent runs the code, searches, and queries catalogues *itself*, instead of you ferrying things in and out. |
| Chatbot / "the model" | **Agent** | A model wrapped in a role: tools + memory + standing rules + guardrails. |
| "Check your work, please" | **Reflection** | The agent critiques and revises its own output — the bridge pattern you already use in chat. |
| Re-explaining yourself each session | **The constitution + memory** | Standing instructions and notes saved to disk, so you don't repeat yourself. |
| "It just made that up" | **Hallucination → verification** | The fix isn't trust; it's a step that checks claims/citations against a real source and blocks what fails. |
| Letting it "just do everything" | **Autonomy dial** | You choose per task: fire-and-forget for low stakes, approve-before-action for high stakes. |
| Author = also the reviewer | **Critic / fixer separation** | A read-only critic finds faults; a separate fixer repairs them; the critic re-checks. Peer review, automated. |

**Mini-diagram to put on the handout:**

```
   You ──▶ Task spec ──▶ Agent loop ──▶ Tools / data ──▶ Output ──▶ Quality gate ──▶ You approve
                              ▲                                          │
                              └──────────── revise if it fails ──────────┘
```

---

*Companion handouts to build next:* `quality-gate-card.md` (≤10 checks, green/yellow/red — the
"should I trust this output?" card) and `cheat-sheet.md` (3–5 research-relevant agent patterns with
task-spec starter templates).
