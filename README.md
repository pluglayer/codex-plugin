# PlugLayer Codex Plugin

This plugin connects Codex to PlugLayer through the published `pluglayer-mcp` package and bundles the PlugLayer deploy and diagnostics skills into one local Codex plugin.

## One-line install

```bash
curl -fsSL https://raw.githubusercontent.com/pluglayer/codex-plugin/main/install.sh | bash
```

The installer gives the user a branded PlugLayer terminal flow, stages the plugin into the Codex personal marketplace, saves the PlugLayer token once, and supports reinstall or token-only updates later.

## What is included
- `.codex-plugin/plugin.json`
  - the Codex plugin manifest
- `.mcp.json`
  - the PlugLayer MCP server definition
- `skills/`
  - deploy apps
  - inspect repos before deploy
  - fix failed deploys
  - configure domains
  - set up CI/CD

## Requirements
1. `uvx` must be available where Codex runs.
2. `pluglayer-mcp` must be resolvable by `uvx`.
3. You need a PlugLayer API token from [portal.pluglayer.com/tokens](https://portal.pluglayer.com/tokens).
4. You need a PlugLayer API token from [portal.pluglayer.com/tokens](https://portal.pluglayer.com/tokens).

## Installer behavior

- Copies the plugin into `~/.agents/plugins/plugins/pluglayer-codex-plugin`
- Creates or updates `~/.agents/plugins/marketplace.json`
- Installs the plugin through `codex plugin add ...` so it is available globally in Codex
- Wires the PlugLayer MCP server into Codex
- Detects the installed version and offers:
  - update/reinstall PlugLayer for Codex
  - update the saved token only

## Local install from this repo

```bash
./install.sh
```

## Install in Codex
Run the one-line installer above, then launch Codex with `codex-pluglayer` or reopen Codex normally if your shell already loads `~/.local/bin`.

## Manual installation checklist
1. Create a PlugLayer API token in [portal.pluglayer.com/tokens](https://portal.pluglayer.com/tokens).
2. Export it in the environment that launches Codex:

```bash
export PLUGLAYER_API_KEY="plk_your_token_here"
```

3. Verify the MCP package is available:

```bash
uvx pluglayer-mcp --help
```

4. Install the plugin from this repository root.
5. Confirm the PlugLayer MCP server connects successfully.
6. Start with one of the prompts below.

## MCP configuration used by this plugin

```json
{
  "pluglayer": {
    "command": "pluglayer-mcp launcher",
    "type": "stdio",
    "args": ["..."]
  }
}
```

## Good first prompts
- "Inspect this repo and tell me whether I should deploy it with Dockerfile or docker-compose."
- "Create a PlugLayer project for this repo and deploy it."
- "Build this repo, deploy it to PlugLayer, and use the default domain for now."
- "Set up GitHub Actions CI/CD for this already-deployed app."
- "Help me attach my custom domain and explain exactly what to put in my DNS provider."
- "Why did this PlugLayer deploy fail? Check logs and fix it."

## Current scope
This plugin is strongest for:
- local repos that need a local image build before deploy
- existing Docker images
- Dockerfile-backed repos
- docker-compose decomposition
- Data Layer database provisioning and wiring
- CI/CD setup for an existing PlugLayer app id
- failure diagnosis using PlugLayer logs plus local repo inspection
- custom domain onboarding and verification help

For DNS-heavy flows, the plugin should translate PlugLayer's exact DNS names into registrar-friendly host entries when needed, such as `@` for the root domain or `_pluglayer-verify` instead of `_pluglayer-verify.example.com` in GoDaddy-style UIs.

It does not expose PlugLayer admin-only tools. The MCP surface is focused on what an end user needs to ship and operate their own apps. Compute stays read-only through MCP, users can remove their own apps, and project removal remains an end-user project workflow rather than an admin action.

## Troubleshooting
- If Codex cannot connect to PlugLayer MCP, rerun the installer or choose the token update option.
- If `uvx pluglayer-mcp` fails, repair the published `pluglayer-mcp` package first.
- If you change `.codex-plugin/plugin.json`, `.mcp.json`, or any skill files, reload Codex so the plugin metadata refreshes.
