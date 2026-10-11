# PlugLayer Codex Plugin

This plugin packages PlugLayer skills and the portable Agent Plugins manifest with the hosted MCP service. No Python, uv, Node, Docker, Git, terminal command, or PlugLayer desktop app is required.

## Setup

1. Open **Setup** in the PlugLayer portal.
2. Choose Codex and copy the prompt.
3. Paste it into Codex.
4. When Codex opens the browser, sign in to PlugLayer and approve OAuth.

The root `plugin.json` and `mcp.json` are the portable package entrypoints. The legacy `.codex-plugin/` manifest remains for older Codex clients. The plugin uses `https://mcp.pluglayer.com/mcp` with OAuth. Tokens are issued and refreshed by PlugLayer and remain in Codex's secure connection storage; no API token is pasted into chat.

The plugin includes PlugLayer MCP plus skills for repo inspection, deployment, domains, CI/CD, project metadata, environment updates, feedback, and deployment repair. Local repository and Docker actions use Codex's own capabilities.
