---
name: eng-questions
description: >-
  Asks at most 2–3 redesign-blocker questions in chat before a design brief is
  written. Use when the user runs /eng-questions or needs a preflight
  clarification pass for /dsgn-refresh.
disable-model-invocation: true
---

# /eng-questions

Preflight slice of **dsgn-refresh**. Read and follow [../dsgn-refresh/SKILL.md](../dsgn-refresh/SKILL.md) working rules.

## Purpose

Surface **blocker** clarifications for the engineer who built the feature **before** the shared brief is generated. This improves brief quality. It is **not** a section inside `docs/design-briefs/`.

## Do

1. Require a free-text feature name (ask once if missing).
2. Skim the codebase (and any existing brief) for gaps that would weaken Intent, Flows, or Locked vs flexible.
3. Ask **at most 2–3** questions **in chat** as **multiple choice** (A/B/C… + Other/note when useful). Follow the preflight format in `dsgn-refresh`. Stop and wait for answers.
4. If nothing critical is unclear, say so in chat — do not invent filler questions.
5. **Do not** add or keep an “Eng questions” section in the Markdown brief.
6. After answers (or a clean skip), tell the runner to run `/dsgn-refresh <feature>` (or offer to continue into it if they ask).
