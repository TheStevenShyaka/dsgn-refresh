# dsgn-refresh

A **Cursor Agent skill** that turns an already-built feature into a short, shareable **design brief** (intent + flows).

Built for teams that ship **build-first**: engineering implements from a light stakeholder brief, then design redesigns to a senior product-design bar. This skill recovers the product story from the **codebase** so designers are not guessing from a staging link alone.

---

## Why this exists

A common workflow looks like this:

1. Little or no product-design discovery up front  
2. Devs build with agents from a boss/stakeholder ask  
3. Features get validated in code  
4. Design gets a staging link and is asked to “make it good”

That handoff is thin. Designers need **what problem this solves**, **how the flow works today**, and **what is locked vs flexible** — without a fake full PRD, and without needing every junior designer to dig through the repo.

`/dsgn-refresh` is the late-stage brief for that moment.

**It is not:** discovery theater, a standards audit, a boss interview script, or Jira cleanup.

---

## Who runs it / who reads it

| Role | Role in the workflow |
|------|----------------------|
| **Engineer (or anyone with Cursor + the repo)** | Runs `/dsgn-refresh <feature>` against the codebase |
| **Design lead + juniors** | Use the Markdown brief + staging to redesign and validate |

The **source of truth for the skill** is the codebase. Staging stays how designers **judge** the UI. The brief is written so people **without repo access** can use it.

---

## What you get

One Markdown file:

```text
docs/design-briefs/<feature-slug>-brief.md
```

Header (keep thin):

- **Scope**
- **Confidence**

Body:

1. **Problem / job** — who, when, done when (`Observed` / `Inferred`)  
2. **Intent** — what the feature is trying to achieve  
3. **Flows** — happy path + key branches (screen names + CTAs, not file paths)  
4. **Locked vs flexible** — what redesign must respect vs can reshape  
5. **Assumptions**

Juniors can open the `.md` in Drive/Docs/Notion later; they do not need Cursor.

**Eng questions are not in the brief.** They are a chat preflight (max 2–3) so the agent can fill gaps before writing the file.

---

## Commands

| Command | What it does |
|---------|----------------|
| **`/dsgn-refresh <feature>`** | Main command — preflight if needed, then full short brief |
| `/feature-intent <feature>` | Problem/job + Intent only |
| `/feature-flows <feature>` | Flows only |
| `/eng-questions <feature>` | Preflight only — ask ≤2–3 questions in chat (no brief section) |

Feature scope is **free text**, e.g. `onboarding`, `month review hero`, `onboarding paywall`.

---

## Install (Cursor project)

Copy the skills into a project (or personal skills folder):

```text
.cursor/skills/dsgn-refresh/
.cursor/skills/feature-intent/
.cursor/skills/feature-flows/
.cursor/skills/eng-questions/
```

From this repo:

```bash
# from your app repo root
cp -R path/to/dsgn-refresh/.cursor/skills/* .cursor/skills/
```

Reload Cursor if the `/` menu does not show the new skills yet.

Then in Agent chat:

```text
/dsgn-refresh onboarding
```

---

## How it works (for the agent)

1. Take the free-text feature name  
2. Search the **codebase** (routes, screens, copy, state, comments)  
3. Draft intent + flows privately; label claims `Observed` vs `Inferred`  
4. **If blockers remain:** ask at most 2–3 eng questions **in chat** and **wait**  
5. Fold answers into the draft  
6. Write `docs/design-briefs/<slug>-brief.md` from `template.md` (no Eng questions section)  
7. Reply with the file path + confidence (not the whole brief)

**Rules that matter:**

- Code is truth — not messy tickets or chat history  
- No fake stakeholder goals  
- No file-path / “code map” dumps in the shared brief  
- Eng questions improve the brief; they are not designer-facing output  

Full instructions live in [`.cursor/skills/dsgn-refresh/SKILL.md`](.cursor/skills/dsgn-refresh/SKILL.md).

---

## Suggested team loop

1. Eng finishes a foundation slice of a feature  
2. Eng runs `/dsgn-refresh <feature>` (answers 2–3 chat questions if the agent asks)  
3. Eng shares the Markdown brief (and staging link) with design  
4. Design redesigns against intent + flows + locked constraints  
5. Quick design validation as usual  

---

## Versioning

- **v1** — intent + flows brief; designer-facing Markdown; codebase as source of truth; eng preflight in chat  
- **Later** — design-standards checklist, clearer ticket templates, optional Notion/Drive export  

This repo is the shareable home for the skill while teams try it on real products.

---

## License

MIT — use it, fork it, adapt the brief shape to your design team.
