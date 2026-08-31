# InstantDM Instagram plugin

Packages InstantDM's hosted Instagram MCP server with the `instagram-manager` skill for Claude Code, ChatGPT, and Codex.

## What's inside

| File | Role |
|---|---|
| `.codex-plugin/plugin.json` | OpenAI / Codex plugin manifest (ChatGPT + Codex directory listing) |
| `.claude-plugin/plugin.json` | Claude Code plugin manifest |
| `.mcp.json` | Hosted MCP server: `https://openapi.instantdm.com/mcp` |
| `skills/instagram-manager/SKILL.md` | Comment triage, inbox follow-up, weekly insights, ad-comment monitoring |
| `assets/logo.png` | Plugin icon |

Auth is an InstantDM API key from [app.instantdm.com/api-integration](https://app.instantdm.com/api-integration), passed as `INSTANTDM_API_KEY` (Codex / Claude) or `Authorization: Bearer <key>` (HTTP).

## Install

**Codex**

```bash
codex plugin marketplace add sanjaykhanssk/instagram-mcp
```

Then install **InstantDM** from the Plugins Directory and set `INSTANTDM_API_KEY`.

**Claude Code**

```
/plugin marketplace add sanjaykhanssk/instagram-mcp
/plugin install instantdm-instagram
```

**ChatGPT (public directory)** — after OpenAI review, install from [chatgpt.com/plugins](https://chatgpt.com/plugins). Until then, add the MCP URL in Developer mode:

```
https://openapi.instantdm.com/mcp?auth=<your-api-key>
```

See the repo README for tool list, credit rules, and the public-directory submission notes.
