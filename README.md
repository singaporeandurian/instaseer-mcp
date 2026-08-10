# InstaSeer MCP Server

Instagram / TikTok / Facebook audience analysis for AI agents. A **hosted remote MCP server** —
nothing to install or run: paste one URL into your client and sign in.

```
Endpoint:   https://www.instaseer.com/mcp
Transport:  Streamable HTTP (stateless)
Auth:       OAuth 2.1 (RFC 9728 discovery, DCR, PKCE) or bearer API keys
Registry:   com.instaseer/mcp
```

## Connect

**Claude (claude.ai / Desktop)** — Settings → Connectors → *Add custom connector* → paste
`https://www.instaseer.com/mcp` → sign in when prompted. Done.

**ChatGPT** — Settings → Apps & Connectors → Developer mode → *Create connector* → same URL,
authentication OAuth.

**Claude Code**
```bash
claude mcp add --transport http instaseer https://www.instaseer.com/mcp \
  --header "Authorization: Bearer YOUR_API_KEY"
```

**Cursor / VS Code / any mcp.json client**
```json
{ "mcpServers": { "instaseer": {
  "type": "http", "url": "https://www.instaseer.com/mcp",
  "headers": { "Authorization": "Bearer YOUR_API_KEY" } } } }
```

API keys (for CLI/editor clients) are created at [instaseer.com/mcp](https://www.instaseer.com/mcp) —
a free account takes a minute and includes 50 credits/month plus unlimited free lookups.

## Tools

| Tool | Returns | Cost |
|---|---|---|
| `instaseer_follower_count` | Live public follower count, following, posts, verification, engagement rate | Free · 100 fresh lookups/day |
| `instaseer_profile_preview` | Headline public profile fields | Free |
| `instaseer_profile_timeline` | Full public post timeline, per-post engagement, posting calendar | ~1 credit/post, min 50 |
| `instaseer_compare_profiles` | Up to 5 handles side by side | Credits per handle |
| `instaseer_account_usage` | Plan, credits used and remaining | Free |

Timeline and compare results include a `viewFullReport` link that opens the same search as a full
web report (source-linked post list, AI summary, CSV export) at no extra cost.

## Example prompts

- "How many followers does @nike have on Instagram right now?"
- "Analyze @glossier's last 100 posts — what's their posting cadence and best-performing content?"
- "Compare @glossier and @sephora and tell me who gets stronger engagement."

## Pricing

MCP usage draws from the same credit balance as the [InstaSeer web app](https://www.instaseer.com):
Free (50 credits/mo), Creator ($9 · 1,500), Plus ($29 · 5,000), Pro ($99 · 18,000), plus one-time
credit packs that never expire. When an agent runs out mid-conversation, the tool result includes a
checkout link — no dead ends.

## Data boundaries (honest by design)

All data comes from what platforms show **logged-out visitors**. Private accounts are never
accessed. Instagram publishes no follower lists to logged-out visitors, so no tool can determine
which followers are real — engagement rate is returned as a plain number, never an
audience-quality verdict.

## Links

- Install page & API keys: https://www.instaseer.com/mcp
- Setup guide: https://www.instaseer.com/instagram-analysis-in-claude-chatgpt
- Pricing: https://www.instaseer.com/pricing · Terms: /terms · Privacy: /privacy
- Support: https://www.instaseer.com/contact
