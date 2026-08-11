# Design brief: {{FEATURE_NAME}}

- **Scope:** {{FEATURE_NAME}}
- **Confidence:** {{HIGH|MEDIUM|LOW}} — short note (no repo jargon)

## Problem / job

Who this seems to help, in what moment, and what “done” looks like.

- **Who:** …
- **When:** …
- **Done when:** …

Label each bullet `Observed` or `Inferred`.

## Intent

What this feature is trying to achieve (product outcome, not UI chrome).

- …
- …

Label each bullet `Observed` or `Inferred`. Do not invent stakeholder strategy.

## Flows

### Happy path

1. …
2. …

Use **screen names and user-visible actions**, not file paths or route strings.

### Key branches

| Branch | What happens |
|--------|----------------|
| Empty / first use | … |
| Error / failure | … |
| Permission / auth gate | … |
| Other (only if real) | … |

## Locked vs flexible

| Area | Status | Why it matters for redesign |
|------|--------|-----------------------------|
| … | Locked | … |
| … | Flexible | … |

**Locked** = hard to change without eng/product cost (required steps, roles, persisted data, must-not-break behavior).
**Flexible** = presentation, copy, layout, empty/error framing design can reshape.

## Assumptions

Guesses that still need a human check. Prefer fewer, sharper items.
Do **not** list unanswered eng questions here — those were resolved in the chat preflight (or skipped).
Say **designers** when referring to readers — not juniors or other titles.
If mentioning how to redesign, prefer: “Redesign from this brief together with the live-link.” Never say “you do not need the repo.”

1. …
2. …
