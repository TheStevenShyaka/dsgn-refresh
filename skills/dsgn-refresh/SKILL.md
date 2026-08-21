---
name: dsgn-refresh
description: >-
  Writes a design brief from the codebase for a named, already-built feature,
  saved under docs/design-briefs/. Use when the user runs /dsgn-refresh, asks
  for a design refresh brief, or needs designers to redesign from what the
  product actually does. Works in Cursor, Claude Code, and similar agents
  that load SKILL.md packs.
disable-model-invocation: true
---

# /dsgn-refresh

Reads the repo and writes one short Markdown file so designers can redesign from this doc and the live-link they already have.

Use it after the feature already exists. Skip standards audits, boss interviews, and Jira cleanup.

## When invoked

The user gives a free-text feature name. That name is required. Examples: `/dsgn-refresh onboarding paywall` or "month review hero".

If the name is missing, ask once, then continue.

## Source of truth

| Source | Role |
|--------|------|
| Codebase | Required. The only trusted source |
| Comments in code | Hints. Check them against real routes, UI, and state |
| Eng answers in chat | Preflight that improves the brief. Do not paste them as a Q&A section |
| Live-link | What designers open to judge the UI. This skill does not have to record it |
| Slack / Linear / Jira / chat history | Ignore for v1 unless the user pastes text into the prompt |

Never invent ticket history or stakeholder goals that are not in the code or in answers the eng runner gives.

## Working rules

1. **Code is truth.** Prefer routes, screens, components, copy, state, and API usage over any story from outside the repo.
2. **Label evidence.** Every material claim is `Observed` if it is in code, or `Inferred` if it is a reasonable guess. After eng answers, upgrade clarified items to `Observed` from eng, or put them in Locked vs flexible. Do not leave open questions in the doc.
3. **Comments help. Do not worship them.** AI and dev comments can be wrong. Check the behavior.
4. **No fake tickets.** Do not invent Jira or Slack context.
5. **Eng questions are a preflight, not an output section.** Ask 2 or 3 blocker questions in chat before writing the brief, never more. Use multiple choice, A/B/C. Wait for answers. Never put an "Eng questions" section in the Markdown.
6. **Write for designers.** Plain language for flows and intent. Say designers, not juniors, leads, or other titles. Do not add lines like "you do not need the repo."
7. **Keep the repo out of the brief.** Use the repo to extract truth. Do not put file paths, route strings like `/(auth)/…`, or a code map in the Markdown. Name screens and user actions instead.
8. **Ship a file.** Always write Markdown to disk, not chat-only, and only after the preflight is done or skipped because nothing critical is unclear.
9. **One feature.** Stay inside the named scope. Do not boil the whole app.
10. **Keep the brief header thin.** Only Scope and Confidence. Do not add a generated date or live-link fields.
11. **Say live-link, not staging.** When you mean the built app designers open, say live-link.

## Workflow

Copy and track:

```
/dsgn-refresh progress:
- [ ] 1. Scope + slug
- [ ] 2. Locate code
- [ ] 3. Draft intent + flows + locked/flexible (private)
- [ ] 4. Preflight eng questions (chat), or skip if clear
- [ ] 5. Fold answers into the draft
- [ ] 6. Write Markdown file
- [ ] 7. Point user at the file path
```

### 1. Scope + slug

- Feature name = user free text.
- Slug = lowercase, hyphenated, filesystem-safe. Example: `Onboarding Paywall` becomes `onboarding-paywall`.
- Output path: `docs/design-briefs/<slug>-brief.md`. Create `docs/design-briefs/` if needed.
- If that file already exists, overwrite with a fresh brief and keep the same path.

### 2. Locate code

Search the workspace for the feature: routes, screen names, components, domain terms in the free-text name.

Prefer the app package the feature lives in. Touch backend only when behavior depends on API or roles. Use those roots privately while extracting. Do not list them in the shared brief.

Read enough to cover entry points, main UI, navigation, empty/error/auth branches, and key comments. Stop when the happy path and important branches are clear. Do not map the entire product.

If you cannot find the feature at all, ask the user to refine the free-text name before writing a stub brief.

### 3. Draft privately

From code and user-visible copy, draft Problem/job, Intent, Flows, Locked vs flexible, and Assumptions. Prefer "appears to…" for inferred outcomes. No fake research, personas, or boss quotes.

Do not write the Markdown file yet.

### 4. Preflight eng questions, chat only

If a redesign blocker remains, for example primary success state, must-not-break behavior, or an unclear branch, ask 2 or 3 questions in chat to the eng runner, never more.

**Multiple choice is required.** Keep each question easy to answer. Short prompt plus 2 to 4 lettered options. Prefer a product decision over an open essay. Add an Other / note option when the answer might not fit the list.

Example shape:

```text
1. Confirm vs categorize, how should redesign treat these?
   A) One combined inbox
   B) Separate jobs
   C) Other / note: …

2. Product language to standardize on?
   A) Need a category
   B) Needs review
   C) Uncategorized
   D) Other / note: …
```

Accept answers like `1B 2A 3C` or short notes on Other.

**Stop and wait** for answers before writing the brief.

If nothing critical is unclear, skip this step. Do not invent filler questions.

Do not paste these questions into the brief. Their job is to improve coverage for the next step.

### 5. Fold answers in

Use eng answers to correct Intent, Flows, Locked vs flexible, and Assumptions. Remove leftover "confirm with eng…" lines. The shared doc should read as decided enough for design to start.

### 6. Write Markdown file

Write the full brief using [template.md](template.md). Fill every section that applies. Keep the doc short enough for designers to skim.

Do not include:

- design-standards scoring, v1
- Code map / file index
- Eng questions section

If an eng runner needs repo pointers, put a short path list in the chat reply only.

### 7. Reply to the user

In chat, only:

1. Absolute or repo-relative path to the written file
2. One-line confidence note

Do not paste the entire brief into chat unless the user asks.

## Slice commands

If the user runs a slice instead of the full refresh, still use this skill's rules:

| Invoke | Produce / update |
|--------|------------------|
| `/feature-intent` | Problem/job + Intent, plus assumptions that affect intent. Still run preflight if intent is blocked |
| `/feature-flows` | Flows. Still run preflight if a branch is blocked |
| `/eng-questions` | Preflight only: ask 2 or 3 questions in chat, never more. Do not write a brief section |

Prefer `/dsgn-refresh` for the normal handoff.

## Out of scope, v1

- Design standards / gap audit
- Boss or stakeholder interview scripts
- Inventing Jira tickets or discovery plans
