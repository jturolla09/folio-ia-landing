# Integrations setup — Folio AI Instagram pipeline

One-time setup. After this, the pipeline runs end-to-end.

## 1. Instagram account (prerequisite)

Meta only allows API publishing from a **Business or Creator** account.

1. Instagram app → Settings → Account type → switch to **Business** (or Creator).
2. Link it to a **Facebook Page** (create a simple Page if needed).

Without this, no tool can legally auto-publish.

## 2. Composio Instagram MCP

1. Create an account at https://composio.dev and open the dashboard.
2. Add the **Instagram** toolkit and connect your IG Business account through
   Composio's OAuth flow (Meta permission screen).
3. Generate a **Composio API key** (Dashboard → API keys).
4. Note your **Tool Router URL** from the dashboard (looks like
   `https://backend.composio.dev/mcp/<session-id>`).
5. In your local terminal, add the MCP server to Claude Code:

   ```bash
   claude mcp add --transport http instagram-composio \
     "https://backend.composio.dev/mcp/<your-tool-router-url>" \
     --header "x-api-key: <YOUR_COMPOSIO_API_KEY>"
   ```

6. Restart Claude Code. Search tools for `instagram` to confirm a
   publish/create-post tool appears.

Docs: https://composio.dev/toolkits/instagram/framework/claude-code

## 3. Asset production — free tools, no subscriptions

Claude generates all the creative content. The only manual step is assembling
the visual file before publishing.

### Carrossel → Canva (free)
- Open canva.com → "Instagram Post" template (square or portrait).
- Apply brand colors: background `#19276a` (cobalt) or `#F5F1E8` (cream).
- Paste the slide texts from the Notion card (already written by Claude).
- Export 6 slides as JPEG images.
- Upload to Google Drive or any public URL and paste the links back to Claude.

### Reel → CapCut (free)
- Open capcut.com (web) or CapCut app (mobile/desktop, free).
- Choose a "texto animado" template with a dark background.
- Follow the scene breakdown in the Notion card (written by Claude).
- Paste the on-screen text per scene as specified.
- Apply brand font (General Sans if available, or the closest clean sans-serif).
- Export vertical 9:16, minimum 720p.
- Upload to Google Drive (or any public URL) and paste the link back to Claude.

Total time per asset: ≤ 5 minutes with the script ready.

## 4. Optional: unattended auto-publish

By default the pipeline stops for your approval before posting. To skip the
approval gate in scheduled runs (only once you trust the output):

```bash
export FOLIO_IG_AUTOPUBLISH=true
```

Leave it unset to keep the approval gate active.

## 5. Scheduling the pipeline

**Option A — Claude Code web trigger (Mon / Wed / Fri, 9h BRT):**
Set up a scheduled session on the repo that runs:
> "Use the folio-ig-pipeline skill to publish the next due post."

**Option B — `/loop` in an interactive session:**
```
/loop 24h Use the folio-ig-pipeline skill to publish the next due post.
```

**Option C — cron + Claude Code CLI (local machine):**
```cron
0 9 * * 1,3,5  cd /path/to/folio-ia-landing && claude -p \
  "Use the folio-ig-pipeline skill to publish the next due post."
```

## What you need before the first run

- [ ] IG Business/Creator account + linked Facebook Page
- [ ] Composio account + API key + Instagram connected via OAuth
- [ ] `claude mcp add` command run (step 2 above)
- [ ] Skills installed: `cp -r skills/* ~/.claude/skills/`
