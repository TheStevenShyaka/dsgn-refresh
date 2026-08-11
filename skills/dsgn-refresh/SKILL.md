---
name: dsgn-refresh
description: >-
  Builds a late-stage design brief (intent + flows) from the codebase for a
  free-text feature name, and writes a shareable Markdown file under
  docs/design-briefs/. Use when the user runs /dsgn-refresh, asks for a design
  refresh brief, or needs designers to redesign an already-built feature from
  repo evidence. Works with any AI coding agent that can load SKILL.md packs
  (Cursor, Claude Code, and similar).
disable-model-invocation: true
---

# /dsgn-refresh

Portable AI-agent skill (not tied to one IDE). Dev-runnable, **codebase-first** brief for design. Produces one short Markdown file so designers can redesign from (1) this doc and (2) staging they already have.

Not a standards audit. Not a boss interview. Not discovery theater. Not Jira cleanup.

## When invoked

User provides a **free-text feature name** (required), e.g. `/dsgn-refresh onboarding paywall` or “month review hero”.

If the feature name is missing, ask once for it, then continue.

## Source of truth

| Source | Role |
|--------|------|
| **Codebase** | Required. Only trusted source |
| Comments in code | Helpful hints — verify against real routes/UI/state |
| Eng answers (chat) | Preflight clarifications that improve the brief — not pasted as a Q&A section |
| Staging / preview | For designers judging the UI — not an input this skill must record |
| Slack / Linear / Jira / chat history | Ignore for v1 unless the user pastes text into the prompt |

Never invent ticket history or stakeholder goals that are not evidenced in code (or in answers the eng runner gives).

## Working rules

1. **Code is truth** — prefer routes, screens, components, copy, state, and API usage over any external story.
2. **Label evidence** — every material claim is `Observed` (in code) or `Inferred` (reasonable guess). After eng answers, upgrade clarified items to `Observed` (from eng) or fold into Locked/Flexible without leaving open questions in the doc.
3. **Comments help, don’t worship them** — AI/dev comments can be wrong; cross-check behavior.
4. **No fake tickets** — do not invent Jira/Slack context.
5. **Eng questions are a preflight, not an output section** — ask at most 2–3 blocker questions **in chat before writing the brief**. Wait for answers. Never put an “Eng questions” section in the Markdown.
6. **Write for designers** — plain language flows and intent. Most readers do **not** have repo access.
7. **No codebase dump in the brief** — use the repo to extract truth, but do **not** put file paths, route strings (`/(auth)/…`), or a “code map” in the Markdown. Name screens and user actions instead.
8. **Ship a file** — always write Markdown to disk (not chat-only), only after the preflight is done (or skipped because nothing critical is unclear).
9. **One feature** — stay inside the named scope; do not boil the whole app.
10. **Brief header stays thin** — only **Scope** and **Confidence**. Do not add Generated date or Staging/preview fields.

## Workflow

Copy and track:

```
/dsgn-refresh progress:
- [ ] 1. Scope + slug
- [ ] 2. Locate code
- [ ] 3. Draft intent + flows + locked/flexible (private)
- [ ] 4. Preflight eng questions (chat) — or skip if clear
- [ ] 5. Fold answers into the draft
- [ ] 6. Write Markdown file
- [ ] 7. Point user at the file path
```

### 1. Scope + slug

- Feature name = user free text.
- Slug = lowercase, hyphenated, filesystem-safe (e.g. `Onboarding Paywall` → `onboarding-paywall`).
- Output path: `docs/design-briefs/<slug>-brief.md` (create `docs/design-briefs/` if needed).
- If that file already exists, overwrite with a fresh brief and keep the same path.

### 2. Locate code

Search the workspace for the feature (routes, screen names, components, domain terms in the free-text name).

Prefer the app package the feature lives in; touch backend only when behavior depends on API/roles. Use those roots privately while extracting — do not list them in the shared brief.

Read enough to cover: entry points, main UI, navigation, empty/error/auth branches, and key comments. Stop when the happy path and important branches are clear — do not map the entire product.

If you cannot find the feature at all, ask the user to refine the free-text name **before** writing a stub brief.

### 3. Draft privately

From code + user-visible copy, draft Problem/job, Intent, Flows, Locked vs flexible, and Assumptions. Prefer “appears to…” for inferred outcomes. No fake research, personas, or boss quotes.

Do **not** write the Markdown file yet.

### 4. Preflight eng questions (chat only)

If a redesign blocker remains (e.g. primary success state, must-not-break behavior, unclear branch), ask **at most 2–3** questions in chat to the eng runner. Questions must be answerable in a few minutes.

**Stop and wait** for answers before writing the brief.

If nothing critical is unclear, skip this step — do not invent filler questions.

Do not paste these questions into the brief. Their job is to improve coverage for the next step.

### 5. Fold answers in

Use eng answers to correct Intent, Flows, Locked vs flexible, and Assumptions. Remove “confirm with eng…” leftovers. The shared doc should read as decided enough for design to start.

### 6. Write Markdown file

Write the full brief using [template.md](template.md). Fill every section that applies; keep the doc short enough for three designers to skim.

Do not include:
- design-standards scoring (v1)
- Code map / file index
- Eng questions section

If an eng runner needs repo pointers, put a short path list in the **chat reply only**.

### 7. Reply to the user

In chat, only:

1. Absolute or repo-relative path to the written file
2. One-line confidence note

Do not paste the entire brief into chat unless the user asks.

## Slice commands

If the user runs a slice instead of full refresh, still use this skill’s rules:

| Invoke | Produce / update |
|--------|------------------|
| `/feature-intent` | Problem/job + Intent (+ assumptions that affect intent) — still run preflight if intent is blocked |
| `/feature-flows` | Flows — still run preflight if a branch is blocked |
| `/eng-questions` | Preflight only: ask ≤2–3 questions in chat; do not write a brief section |

Prefer `/dsgn-refresh` for the normal handoff.

## Out of scope (v1)

- Design standards / gap audit
- Boss or stakeholder interview scripts
- Inventing Jira tickets or discovery plans
