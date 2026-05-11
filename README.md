# PlugLayer Codex Plugin

This plugin connects Codex to PlugLayer using the published `pluglayer-mcp` package.

## What it includes
- PlugLayer MCP wiring via `.mcp.json`
- Skills for:
  - repo inspection
  - deployment to PlugLayer
  - deployment failure diagnosis
  - custom domain guidance

## Requirements
1. `pluglayer-mcp` must be available through `uvx`
2. You need a PlugLayer API token from the PlugLayer Settings page
3. Export the token before launching Codex:

```bash
export PLUGLAYER_API_KEY="plk_your_token_here"
```

## Install step by step
1. Clone or download this plugin folder.
2. Make sure `uvx` can run `pluglayer-mcp`.
3. Create a PlugLayer API token in the PlugLayer Settings page.
4. Export the token in the shell where you will launch Codex:

```bash
export PLUGLAYER_API_KEY="plk_your_token_here"
```

5. Point Codex at this plugin directory according to your Codex plugin loading flow.
6. Confirm the PlugLayer MCP is connected.
7. Use the included skills to inspect, deploy, debug, and handle domain setup.

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
- "Build this repo, deploy it to PlugLayer, and use the default domain for now."
- "Help me attach my custom domain and explain exactly what to put in my DNS provider."
- "Why did this PlugLayer deploy fail? Check logs and fix it."

## Current scope
This plugin is strongest for:
- current local repos that need a local image build before deploy
- existing Docker images
- Dockerfile-backed repos
- docker-compose deployments
- failure diagnosis using PlugLayer logs plus local repo inspection
- end-user compute selection through PlugLayer marketplace
- custom domain onboarding and verification help

It does not expose PlugLayer admin-only tools. The MCP surface is focused on what an end user needs to ship and operate their own apps, including archiving their own apps and projects while leaving compute administration out of scope.
