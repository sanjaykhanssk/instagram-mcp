# List InstantDM in the OpenAI Plugins Directory

This repo is packaged as an OpenAI plugin for ChatGPT and Codex, following
[Package your plugin](https://developers.openai.com/plugins/build/plugins).

```
plugins/instantdm-instagram/
  .codex-plugin/plugin.json   required manifest
  .mcp.json                   hosted MCP server
  skills/instagram-manager/   workflows
  assets/logo.png             listing icon
.agents/plugins/marketplace.json
```

## Codex (works now)

```bash
codex plugin marketplace add sanjaykhanssk/instagram-mcp
```

Install **InstantDM** from the Plugins Directory. Set `INSTANTDM_API_KEY` from
[app.instantdm.com/api-integration](https://app.instantdm.com/api-integration).

## ChatGPT public directory

OpenAI reviews public listings. Publishing a local/workspace plugin does **not**
put InstantDM in the universal directory.

1. Open the [plugin submission portal](https://developers.openai.com/plugins/deploy/submission).
2. **Create plugin** → **With MCP** (MCP + uploaded skills).
3. MCP server URL: `https://openapi.instantdm.com/mcp`
4. Upload `plugins/instantdm-instagram/` (or a zip of that folder). The portal
   accepts `.codex-plugin/plugin.json` or `.claude-plugin/plugin.json`.
5. Fill listing fields from `.codex-plugin/plugin.json` (`interface.*`).
6. Starter prompts are already in `interface.defaultPrompt`.
7. Attest policies and **Submit for Review**. After approval, publish from the portal.

### Auth

ChatGPT's public directory expects [OAuth 2.1](https://developers.openai.com/plugins/build/auth)
on the MCP server. It does not accept custom API keys. Developer mode and Codex
can use `INSTANTDM_API_KEY` / `?auth=` today. For directory approval, add MCP
OAuth on `openapi.instantdm.com` (protected resource metadata + authorization
server), then resubmit.

Do **not** submit an existing ChatGPT app/integration by reference — submit the
MCP server as a new plugin.

## Zip for the portal

From the plugin folder:

```bash
cd plugins/instantdm-instagram
zip -r ../../instantdm-instagram-openai.zip .codex-plugin .mcp.json skills assets README.md
```

The zip root (or its single top-level directory) must contain
`.codex-plugin/plugin.json` or `.claude-plugin/plugin.json`.
