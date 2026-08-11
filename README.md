# dsgn-refresh

An **AI agent skill pack** that turns an already-built feature into a short, shareable **design brief** (intent + flows).

Works with **any AI coding agent** that can load skill / instruction packs — including **Claude Code**, **Cursor**, and similar tools. The Markdown under `skills/` is the product; the host app is just how you invoke it.

Built for teams that ship **build-first**: engineering implements from a light stakeholder brief, then design redesigns to a senior product-design bar. This skill recovers the product story from the **codebase** so designers are not guessing from a staging link alone.

---

## Why this exists

A common workflow looks like this:

1. Little or no product-design discovery up front  
2. Devs build with agents from a boss/stakeholder ask  
3. Features get validated in code  
4. Design gets a staging link and is asked to “make it good”

That handoff is thin. Designers need **what problem this solves**, **how the flow works today**, and **what is locked vs flexible** — without a fake full PRD, and without needing every junior designer to dig through the repo.

`/dsgn-refresh` (or the same prompt in your agent) is the late-stage brief for that moment.

**It is not:** discovery theater, a standards audit, a boss interview script, or Jira cleanup.

---

## Who runs it / who reads it

| Role | Role in the workflow |
|------|----------------------|
| **Engineer (with the app repo + any supported agent)** | Runs the skill against the codebase |
| **Design lead + juniors** | Use the Markdown brief + staging to redesign and validate |

The **source of truth for extraction** is the **product codebase**. Staging is how designers **judge** the UI. The brief is written so people **without repo access** can use it.

---

## Repo layout

```text
skills/
  dsgn-refresh/     ← main skill + brief template
  feature-intent/   ← optional slice
  feature-flows/    ← optional slice
  eng-questions/    ← chat preflight only
```

Canonical path is **`skills/`**. Copy those folders into whatever skills directory your agent uses.

---

## What you get

One Markdown file in the **product** repo (not this skill repo):

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

Juniors can open the `.md` in Drive/Docs/Notion later; they do not need an AI IDE.

**Eng questions are not in the brief.** They are a chat preflight (max 2–3) so the agent can fill gaps before writing the file.

---

## Commands / invoke names

| Invoke | What it does |
|--------|----------------|
| **`/dsgn-refresh <feature>`** | Main — preflight if needed, then full short brief |
| `/feature-intent <feature>` | Problem/job + Intent only |
| `/feature-flows <feature>` | Flows only |
| `/eng-questions <feature>` | Preflight only — ask ≤2–3 questions in chat (no brief section) |

Feature scope is **free text**, e.g. `onboarding`, `month review hero`.

If your agent has no slash menu, say the same thing in plain language and point it at `skills/dsgn-refresh/SKILL.md`.

---

## Install (any agent)

From this repo, copy the packs into your **product** project’s skills folder:

### Claude Code (common here)

```bash
# from your app repo root
mkdir -p .claude/skills
cp -R path/to/dsgn-refresh/skills/* .claude/skills/
```

Some setups also use `.agents/skills/` — same idea:

```bash
mkdir -p .agents/skills
cp -R path/to/dsgn-refresh/skills/* .agents/skills/
```

### Cursor

```bash
mkdir -p .cursor/skills
cp -R path/to/dsgn-refresh/skills/* .cursor/skills/
```

### Other agents

Copy `skills/*` into whatever directory that tool loads for project skills / custom instructions. The files are plain Markdown (`SKILL.md` + `template.md`).

Then run:

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

Full instructions: [`skills/dsgn-refresh/SKILL.md`](skills/dsgn-refresh/SKILL.md).

---

## Suggested team loop

1. Eng finishes a foundation slice of a feature  
2. Eng runs `/dsgn-refresh <feature>` in their agent (answers 2–3 chat questions if asked)  
3. Eng shares the Markdown brief (and staging link) with design  
4. Design redesigns against intent + flows + locked constraints  
5. Quick design validation as usual  

---

## Developing this skill

This GitHub repo is the **source of truth** for the skill pack. Update here and push as you iterate.

Product apps (e.g. Fundt) may keep a **local copy** under `.cursor/skills/` or `.claude/skills/` only for trying the skill on that codebase. Prefer pulling changes from this repo rather than treating an app’s copy as canonical.

---

## Versioning

- **v1** — intent + flows brief; designer-facing Markdown; codebase as source of truth; eng preflight in chat; agent-agnostic `skills/` layout  
- **Later** — design-standards checklist, clearer ticket templates, optional Notion/Drive export  

---

## License

MIT — use it, fork it, adapt the brief shape to your design team.
