---
name: feature-flows
description: >-
  Maps happy-path and key branches for an already-built feature from the
  codebase into docs/design-briefs/. Use when the user runs /feature-flows
  or only needs the flows slice of a design brief.
disable-model-invocation: true
---

# /feature-flows

Slice of **dsgn-refresh**. Read and follow [../dsgn-refresh/SKILL.md](../dsgn-refresh/SKILL.md) working rules and source-of-truth rules.

## Do

1. Require a free-text feature name (ask once if missing).
2. Locate routes, screens, and branches in the codebase.
3. Document **Flows** (happy path + real key branches) in designer-readable language — screen names and CTAs, not file paths.
4. Write or update `docs/design-briefs/<slug>-brief.md` using [../dsgn-refresh/template.md](../dsgn-refresh/template.md). If the file exists, refresh Flows; if missing, create with those sections filled and stub the rest lightly (`TBD — run /dsgn-refresh for full brief`).
5. Reply with the file path only.
