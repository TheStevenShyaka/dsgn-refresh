---
name: eng-questions
description: >-
  Produces at most 2–3 blocker questions for the engineer who built a feature,
  from codebase gaps or an existing design brief. Use when the user runs
  /eng-questions.
disable-model-invocation: true
---

# /eng-questions

Slice of **dsgn-refresh**. Read and follow [../dsgn-refresh/SKILL.md](../dsgn-refresh/SKILL.md) working rules.

## Do

1. Require a free-text feature name (ask once if missing).
2. Prefer reading an existing `docs/design-briefs/<slug>-brief.md` if present; otherwise skim the codebase for gaps only.
3. Produce **at most 2–3** questions that block redesign (primary user, must-not-break, unclear branch). Skip fluff. If nothing critical is unclear, say so and write `None — code evidence was enough.`
4. Update the Eng questions section in `docs/design-briefs/<slug>-brief.md` (create a minimal file from [../dsgn-refresh/template.md](../dsgn-refresh/template.md) if needed).
5. Reply with the file path and paste the 2–3 questions in chat so the runner can send them to eng.
