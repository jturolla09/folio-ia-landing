# Folio AI — marketing automation skills

Two Claude Code skills for running the Folio AI Instagram campaign and user
emails.

## What's inside

- `folio-ig-pipeline/` — reads the Notion content calendar, generates fresh
  content + a Higgsfield video/carousel, waits for your approval, publishes to
  Instagram via Composio, and marks the post published. Schedulable.
  - `SKILL.md` — the pipeline logic
  - `INTEGRATIONS.md` — one-time setup for Composio (Instagram) + Higgsfield,
    the auto-publish flag, and cron/loop scheduling
- `folio-email-reminder/` — drafts pt-BR re-engagement emails to your user base
  (Gmail drafts or ESP template), with LGPD/opt-out guardrails.

## Install (local Claude Code)

Pick one location:

**Personal (available in every project):**
```bash
mkdir -p ~/.claude/skills
cp -r folio-ig-pipeline folio-email-reminder ~/.claude/skills/
```

**Project-scoped (only in one repo, version-controlled):**
```bash
mkdir -p /path/to/your/repo/.claude/skills
cp -r folio-ig-pipeline folio-email-reminder /path/to/your/repo/.claude/skills/
```

Restart / reopen Claude Code. The skills appear automatically (matched by their
`description`). Invoke them by asking naturally, e.g. "run the Instagram
pipeline" or "draft a reminder to my users", or type `/folio-ig-pipeline`.

## Before they can publish

The pipeline needs two MCP servers connected (see
`folio-ig-pipeline/INTEGRATIONS.md`):
- **Composio Instagram** (needs IG Business/Creator + Facebook Page + Composio API key)
- **Higgsfield** (OAuth, uses plan credits)

The Notion server is referenced by the data-source ID baked into the skill —
if you clone the campaign into a different Notion workspace, update the ID at
the top of `folio-ig-pipeline/SKILL.md`.

Until those are connected, the pipeline still works in "generate + draft into
Notion + tell me what's missing" mode — it just won't auto-post.
