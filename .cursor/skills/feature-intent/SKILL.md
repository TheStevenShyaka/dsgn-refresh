---
name: feature-intent
description: >-
  Extracts Problem/job and Intent for an already-built feature from the
  codebase into docs/design-briefs/. Use when the user runs /feature-intent
  or only needs the intent slice of a design brief.
disable-model-invocation: true
---

# /feature-intent

Slice of **dsgn-refresh**. Read and follow [../dsgn-refresh/SKILL.md](../dsgn-refresh/SKILL.md) working rules and source-of-truth rules.

## Do

1. Require a free-text feature name (ask once if missing).
2. Locate the feature in the codebase (code is required; ignore Jira/Slack unless pasted).
3. Draft **Problem / job** and **Intent** only, with `Observed` / `Inferred` labels.
4. Include assumptions that affect intent; do not invent stakeholder strategy.
5. Write or update `docs/design-briefs/<slug>-brief.md` using [../dsgn-refresh/template.md](../dsgn-refresh/template.md). If the file exists, refresh those sections and leave other sections intact when possible; if missing, create the file with those sections filled and stub the rest lightly (`TBD — run /dsgn-refresh for full brief`).
6. Reply with the file path only (plus eng questions only if intent is blocked without them — max 2–3).
