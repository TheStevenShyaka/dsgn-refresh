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

This slice is a private draft for the person running it. `/dsgn-refresh` is the shareable handoff.

## Do

1. Require a free-text feature name. Ask once if missing.
2. Locate routes, screens, entries, and branches in the codebase.
3. If a key branch is blocked by an unclear product rule, ask 2 or 3 multiple-choice questions in chat, never more, and wait. Ask the person who ran this skill. Do not put the questions in the brief.
4. Document Open in the live-link, Entries, happy path, and real key branches in designer-readable language. Screen names and CTAs, not file paths. No URLs or passwords. Happy path starts at the feature, not at login.
5. Write or update `docs/design-briefs/<slug>-brief.md` using [../dsgn-refresh/template.md](../dsgn-refresh/template.md). If the file exists, refresh those sections. If missing, create it with those sections filled, stub the rest with `TBD. Run /dsgn-refresh for the full brief`, and put `Incomplete. Private draft. Run /dsgn-refresh before sharing.` at the top.
6. Reply with the file path, how to open after login in one line, and say it is incomplete if the file is still a stub.
