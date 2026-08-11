---
name: dsgn-refresh
description: >-
  Builds a late-stage design brief (intent + flows) from the codebase for a
  free-text feature name, and writes a shareable Markdown file under
  docs/design-briefs/. Use when the user runs /dsgn-refresh, asks for a design
  refresh brief, or needs designers to redesign an already-built feature from
  repo evidence.
disable-model-invocation: true
---

# /dsgn-refresh

Dev-runnable, **codebase-first** brief for design. Produces one short Markdown file so designers can redesign from (1) this doc and (2) staging they already have.

Not a standards audit. Not a boss interview. Not discovery theater. Not Jira cleanup.

## When invoked

User provides a **free-text feature name** (required), e.g. `/dsgn-refresh onboarding paywall` or “month review hero”.

If the feature name is missing, ask once for it, then continue.

## Source of truth

| Source | Role |
|--------|------|
| **Codebase** | Required. Only trusted source |
| Comments in code | Helpful hints — verify against real routes/UI/state |
| Staging / preview | For designers judging the UI — not an input this skill must record |
| Slack / Linear / Jira / chat | Ignore for v1 unless the user pastes text into the prompt |

Never invent ticket history or stakeholder goals that are not evidenced in code (or in text the user pasted).

## Working rules

1. **Code is truth** — prefer routes, screens, components, copy, state, and API usage over any external story.
2. **Label evidence** — every material claim is `Observed` (in code) or `Inferred` (reasonable guess).
3. **Comments help, don’t worship them** — AI/dev comments can be wrong; cross-check behavior.
4. **No fake tickets** — do not invent Jira/Slack context.
5. **Ask eng only for blockers** — at most 2–3 questions; skip the section if unnecessary.
6. **Write for designers** — plain language flows and intent. Most readers do **not** have repo access.
7. **No codebase dump in the brief** — use the repo to extract truth, but do **not** put file paths, route strings (`/(auth)/…`), or a “code map” in the Markdown. Name screens and user actions instead.
8. **Ship a file** — always write Markdown to disk (not chat-only).
9. **One feature** — stay inside the named scope; do not boil the whole app.
10. **Brief header stays thin** — only **Scope** and **Confidence**. Do not add Generated date or Staging/preview fields.

## Workflow

Copy and track:

```
/dsgn-refresh progress:
- [ ] 1. Scope + slug
- [ ] 2. Locate code
- [ ] 3. Extract intent
- [ ] 4. Map flows
- [ ] 5. Locked vs flexible
- [ ] 6. Assumptions + eng questions
- [ ] 7. Write Markdown file
- [ ] 8. Point user at the file path
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

If you cannot find the feature with reasonable confidence, write a short stub brief that states what was unclear (in product language) and ask the user to refine the free-text name. Still write the file.

### 3. Extract intent

From code + user-visible copy, draft Problem/job and Intent. Prefer “appears to…” for inferred outcomes. No fake research, personas, or boss quotes.

### 4. Map flows

Document happy path and key branches that exist in code (empty, error, permission, and other real branches only). Describe steps with **screen names and CTAs** designers will see in staging — not repo paths.

### 5. Locked vs flexible

- **Locked:** data model, API contracts, required steps, roles/permissions, persistence that redesign must respect.
- **Flexible:** layout, hierarchy, visual treatment, microcopy framing, empty/error presentation — unless code hard-requires a specific sequence.

### 6. Assumptions + eng questions

List sharp assumptions. Add **at most 2–3** eng questions only if a redesign blocker remains (e.g. primary user, must-not-break behavior, unclear branch). Questions must be answerable in a few minutes. If nothing critical is unclear, omit the Eng questions section or leave a single line: `None — product evidence was enough.`

### 7. Write Markdown file

Write the full brief using [template.md](template.md). Fill every section that applies; keep the doc short enough for three designers to skim.

Do not include design-standards scoring in v1.
Do not include a Code map / file index in the brief. If an eng runner needs pointers, put one short path list in the **chat reply only**, not in the shared Markdown.

### 8. Reply to the user

In chat, only:

1. Absolute or repo-relative path to the written file
2. One-line confidence note
3. The 2–3 eng questions (if any) so the runner can paste them to the builder

Do not paste the entire brief into chat unless the user asks.

## Slice commands

If the user runs a slice instead of full refresh, still use this skill’s rules and the same output path when updating a brief:

| Invoke | Produce / update |
|--------|------------------|
| `/feature-intent` | Problem/job + Intent (+ assumptions that affect intent) |
| `/feature-flows` | Flows |
| `/eng-questions` | Eng questions only (max 2–3), from gaps in code or an existing brief |

Prefer `/dsgn-refresh` for the normal handoff.

## Out of scope (v1)

- Design standards / gap audit
- Boss or stakeholder interview scripts
- Inventing Jira tickets or discovery plans
