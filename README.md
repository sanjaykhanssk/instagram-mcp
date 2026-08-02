# InstantDM Instagram MCP Server — Instagram DM & Comment Automation for AI Agents

![Meta Business Partner](https://img.shields.io/badge/Meta-Business%20Partner-0668E1) ![MCP](https://img.shields.io/badge/MCP-Streamable%20HTTP-8A2BE2) ![Hosted](https://img.shields.io/badge/server-hosted%2C%20nothing%20to%20install-2ea44f)

**The Instagram MCP server for Claude, ChatGPT, Codex, OpenClaw, and Hermes Agent.** [InstantDM](https://instantdm.com) is a **Meta Business Partner** building Instagram DM automation on the official Instagram Graph API. This MCP server puts that whole platform inside any AI agent: reply to comments, send DMs, triage your inbox, pull account and post insights, and manage comments on your Meta ads — with your approval on every send.

If you've been looking for a **ManyChat alternative** that AI agents can actually drive — not a flow builder, but a real API your assistant works through — this is it.

**Hosted server. Nothing to install:**

```
https://openapi.instantdm.com/mcp?auth=<your-api-key>
```

Get your API key at **[app.instantdm.com/api-integration](https://app.instantdm.com/api-integration)** (API Keys card → Generate New Key).

## What your AI agent can do

- **Instagram comment automation** — list comments on any post, classify them, and reply publicly or with a private DM to the commenter
- **Instagram DM automation** — read conversations, draft replies in your voice, send after you approve
- **Instagram content publishing** — upload and publish images, reels, stories, and carousels straight from the agent (public media URLs in, live post out)
- **Instagram insights & analytics** — account reach, views, interactions, daily follower counts, audience demographics, and per-post metrics (reels watch time included)
- **Meta ads comment management** — list your ad accounts and ads, read the comments people leave on your ads, and answer them before they burn your ad spend
- **Facebook Page management** — Page feed, Page comments, and replies with the same tools
- **InstantDM automations** — trigger your existing DM flows and tag CRM contacts from the agent

## Connect

**Claude (claude.ai)** — Settings → Connectors → *Add custom connector* → paste the URL above (with your key in it).

**Claude Code**

```bash
claude mcp add --transport http instantdm "https://openapi.instantdm.com/mcp?auth=<your-api-key>"
```

**ChatGPT** — Settings → Apps & Connectors → Developer mode → add the URL above.

**Codex** — add to `~/.codex/config.toml`:

```toml
[mcp_servers.instantdm]
url = "https://openapi.instantdm.com/mcp?auth=<your-api-key>"
```

**OpenClaw / Hermes Agent / any MCP client** — point your agent's MCP configuration at the hosted URL. Standard JSON shape:

```json
{
  "mcpServers": {
    "instantdm": {
      "type": "http",
      "url": "https://openapi.instantdm.com/mcp?auth=<your-api-key>"
    }
  }
}
```

**Claude Code plugin** (MCP connection + the `instagram-manager` skill with ready-made triage, reporting, and ad-monitoring workflows):

```
/plugin marketplace add sanjaykhanssk/instagram-mcp
/plugin install instantdm-instagram
```

Then set `INSTANTDM_API_KEY` in your environment.

## Tools (22)

| Tool | What it does | Cost |
|---|---|---|
| `whoami` | Account, plan, remaining credits — call first | free |
| `list_posts` | Recent posts & reels | free |
| `create_post` | Upload & publish an image, reel, story, or carousel now | 1 credit |
| `publish_post` | Finish publishing a video container still processing | (billed on publish) |
| `list_comments` | Comments on a post | free |
| `reply_to_comment` | Reply publicly or as a private DM (`visibility`) | 1 credit |
| `send_dm` | DM a user | 1 credit |
| `list_conversations` / `get_conversation` | Inbox and message history | free |
| `get_contact_profile` | Commenter/DM-sender profile: username, followers, follows-you | free |
| `get_account_insights` | Reach, views, interactions, follower series, demographics | free |
| `get_post_insights` | Per-post metrics (reels: watch time; stories: navigation) | free |
| `list_ad_accounts` / `list_ads` | Meta ad accounts and ads (with linked IG media) | free |
| `list_ad_comments` | Comments on an ad's Instagram media | free |
| `reply_to_ad_comment` | Reply to ad comments, public or private DM | 1 credit |
| `list_fb_page_posts` / `list_fb_page_comments` | Facebook Page feed & comments | free |
| `reply_to_fb_comment` | Reply to a Page comment | 1 credit |
| `trigger_flow` | Start an InstantDM automation flow for a contact | credits per step |
| `create_or_update_contact` | Tag/update a CRM contact | free |
| `disable_automation` | Pause all InstantDM automations (account-wide) | free |

Reads are free. Anything that sends a message bills **1 InstantDM credit** through your existing plan — the same billing as your automations and the REST API. No per-contact pricing.

## InstantDM vs ManyChat (and other flow builders)

| | **InstantDM MCP** | Flow builders (ManyChat, etc.) |
|---|---|---|
| AI agents (Claude, ChatGPT, Codex, OpenClaw, Hermes) drive it | ✅ Native MCP server | ❌ No MCP support |
| Replies written per-comment, in your voice | ✅ Your agent drafts, you approve | Template blocks |
| Full REST API for every feature | ✅ [openapi.yaml](./openapi.yaml) | Limited API surface |
| Instagram insights via API | ✅ Account + per-post | Dashboard only |
| Meta ads comment management via API | ✅ List + reply | — |
| Pricing model | Flat credits per message sent | Per-contact tiers |
| Built on the official Instagram Graph API | ✅ Meta Business Partner | ✅ |

ManyChat is a fine visual flow builder. InstantDM is what you use when the "flow" is an AI agent having real conversations — and when you want the same capabilities scriptable from make.com, Zapier, or your own backend through one API.

## FAQ

**Is Instagram DM automation allowed?**
Yes — when it's built on the official Instagram Graph API with a Meta-approved app. InstantDM is a Meta Business Partner; every message this server sends goes through Meta's official messaging endpoints, with Instagram's messaging windows and rate limits enforced.

**Can Claude or ChatGPT really manage my Instagram account?**
Yes. Connect the URL above and your assistant can read comments, DMs, insights, and ads, and send replies you approve — the same goes for Codex, OpenClaw, Hermes Agent, or any other MCP-capable agent. The bundled `instagram-manager` skill ships guardrails: it always shows you the exact text and recipient before anything is sent.

**Is this a ManyChat alternative?**
For AI-driven Instagram engagement, yes — see the comparison above. You can also run both: InstantDM's REST API and MCP server work alongside whatever else manages your account.

**What is an MCP server?**
[Model Context Protocol](https://modelcontextprotocol.io) is the open standard AI assistants use to call external tools. This repo documents InstantDM's hosted MCP endpoint — you don't run any code; you just connect the URL with your API key.

**Do I need a Facebook account?**
Instagram Login alone covers posts, comments, DMs, and insights. The **ads tools** need Instagram connected via Facebook Login (Meta's Marketing API requires the Facebook user token) — you'll get a clear `reconnect_required` message otherwise. Facebook Page tools need a connected Page.

## Troubleshooting

| Error | Meaning |
|---|---|
| 401 | Bad or missing API key — regenerate at app.instantdm.com/api-integration |
| 402 | Credits exhausted — top up in the app |
| 403 `upgrade_required` | Plan has no API access |
| 403 `reconnect_required` | Ads tools need Facebook Login connection |
| 429 | Hourly send limit reached — wait for the top of the hour |

Facing an issue, or need an endpoint we don't have yet? [Open an issue](https://github.com/sanjaykhanssk/instagram-mcp/issues) — we ship fast.

## REST API

Every tool is also a plain REST endpoint on `https://openapi.instantdm.com` with `Authorization: Bearer <key>` — see [openapi.yaml](./openapi.yaml). Use it from make.com, Zapier code steps, or your own backend.

---

*Instagram DM automation · Instagram comment automation API · Instagram MCP server · ManyChat alternative · Meta Business Partner · AI Instagram assistant for Claude, ChatGPT, Codex, OpenClaw & Hermes Agent*
