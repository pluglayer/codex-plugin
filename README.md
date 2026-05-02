# PlugLayer Codex Plugin

This plugin connects Codex to PlugLayer using the published `pluglayer-mcp` package.

## What it includes
- PlugLayer MCP wiring via `.mcp.json`
- Skills for:
  - repo inspection
  - deployment to PlugLayer
  - deployment failure diagnosis

## Requirements
1. `pluglayer-mcp` must be available through `uvx`
2. You need a PlugLayer API token from the PlugLayer Settings page
3. Export the token before launching Codex:

```bash
export PLUGLAYER_API_KEY="plk_your_token_here"
```

## MCP configuration used by this plugin

```json
{
  "pluglayer": {
    "command": "uvx",
    "type": "stdio",
    "args": ["pluglayer-mcp"],
    "env": {
      "PLUGLAYER_API_KEY": "${PLUGLAYER_API_KEY}"
    }
  }
}
```

## Good first prompts
- "Inspect this repo and tell me whether I should deploy it with Dockerfile or docker-compose."
- "Create a PlugLayer project for this repo and deploy it."
- "Show me my available compute and tell me whether I can deploy now."
- "Why did this PlugLayer deploy fail? Check logs and fix it."

## Current scope
This plugin is strongest for:
- existing Docker images
- Dockerfile-backed repos
- docker-compose deployments
- failure diagnosis using PlugLayer logs plus local repo inspection
- end-user self-service compute visibility and personal SSH node onboarding

It does not expose PlugLayer admin-only tools. The MCP surface is focused on what an end user needs to ship and operate their own apps.
