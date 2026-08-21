# Design brief: {{FEATURE_NAME}}

- **Scope:** {{FEATURE_NAME}}
- **Confidence:** {{HIGH|MEDIUM|LOW}}, plus a short note with no repo jargon

## Problem / job

Who this seems to help, in what moment, how often, and what done looks like.

- **Who:** …
- **When:** …
- **How often:** once / regular chore / exception
- **Done when:** …

Label each bullet `Observed` or `Inferred`.

## What's awkward

Skip this section if nothing is evidenced in code or copy. At most 3 bullets.

Each bullet points at a screen, CTA, or string. Label `Inferred` unless the invoker confirmed it. No generic usability notes.

- …
- …

## Intent

What this feature is trying to achieve. Product outcome, not UI chrome.

- …
- …

Label each bullet `Observed` or `Inferred`. Do not invent stakeholder strategy.

## Open in the live-link

Designer starts at login. Sessions are short. No URLs, passwords, or environment names.

1. Sign in with the shared designer account
2. After login: …
3. You are in the right place when …

If this feature is login or first-run, say that here and skip the post-login trail.

## Flows

### Entries

How someone reaches this feature after they are in the app. Only real ones: tab, banner, reminder, returning user, and so on.

- …

### Happy path

1. …
2. …

Use screen names and user-visible actions, not file paths or route strings. Start at the feature, not at login.

### Key branches

| Branch | What happens |
|--------|----------------|
| First use | … |
| Empty after success | … |
| Error / failure | … |
| Permission / role gate | … |
| Undo / back, only if real | … |
| Kill and return, only if real | … |
| Other, only if real | … |

Omit a row if that branch does not exist.

## Locked vs flexible

| Area | Status | Why it matters for redesign |
|------|--------|-----------------------------|
| … | Locked | … |
| … | Flexible | … |

**Locked** means changing it has real cost: required steps, roles, persisted data, must-not-break behavior, or a sequence people already know.
**Flexible** means presentation, copy, layout, empty and error framing, mixed jobs you are allowed to split. Do not mark something Locked only because it exists in the build.

## Out of scope for this brief

Adjacent work that showed up in code but is not this job. Omit this section if there is none.

- …

## Assumptions

Guesses that still need a human check. Prefer fewer, sharper items.
Do not list unanswered questions here. Those were resolved in the chat preflight, or skipped.
Say designers when referring to readers.

1. …
2. …
