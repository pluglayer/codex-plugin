# PlugLayer Codex Plugin

This plugin connects Codex to PlugLayer through the published `pluglayer-mcp` package and bundles the PlugLayer deploy and diagnostics skills into one local Codex plugin.

## One-line install

```bash
curl -fsSL https://raw.githubusercontent.com/pluglayer/codex-plugin/main/install.sh | bash
```

The installer gives the user a branded PlugLayer terminal flow, stages the plugin into the Codex personal marketplace, saves the PlugLayer token once, and supports reinstall or token-only updates later. It uses the Codex CLI on `PATH` or the desktop app's embedded CLI to register and verify the exact prepared version. If neither is available, it still updates the personal marketplace source for a later app install.

## What is included
- `.codex-plugin/plugin.json`
  - the Codex plugin manifest
- `.mcp.json`
  - the PlugLayer MCP server definition
- `skills/`
  - deploy apps
  - update project display names and descriptions without changing routing identity
  - inspect repos before deploy
  - fix failed deploys
  - configure domains
  - set up CI/CD
  - securely import runtime env vars from key/value maps or dotenv/JSON/YAML content
  - submit, track, and update the text of safe owned product feedback

## Requirements
1. `uvx` must be available where Codex runs so the PlugLayer MCP can start.
2. `pluglayer-mcp` must be resolvable by `uvx`.
3. You need a PlugLayer API token from [portal.pluglayer.com/tokens](https://portal.pluglayer.com/tokens).

## Installer behavior

- Copies the plugin into `~/plugins/pluglayer-codex-plugin`, the source path Codex resolves for the personal marketplace entry
- Creates or updates `~/.agents/plugins/marketplace.json`
- Uses the `codex` CLI on `PATH` or the desktop app's embedded CLI to install the plugin, verifies the installed cache version, and creates a `codex-pluglayer` launcher
- If no Codex executable can be located, leaves the marketplace and plugin files ready for the app to load after restart and reports that automatic registration could not be verified
- Wires the PlugLayer MCP server into Codex
- Detects the installed version and offers:
  - update/reinstall PlugLayer for Codex
  - update the saved token only
- During normal PlugLayer work, MCP checks installer-managed plugin versions at
  most once per 24 hours. It stays quiet when current, asks before an available
  update, and installs only the exact approved version from a pinned public
  repository commit.

## Local install from this repo

```bash
./install.sh
```

## Install in Codex
Run the one-line installer above. Desktop-only users should fully quit and reopen Codex so it refreshes the personal marketplace. CLI users can also launch Codex with `codex-pluglayer` when the installer created that launcher.

## Manual installation checklist
1. Create a PlugLayer API token in [portal.pluglayer.com/tokens](https://portal.pluglayer.com/tokens).
2. Export it in the environment that launches Codex:

```bash
export PLUGLAYER_API_KEY="plk_your_token_here"
```

3. Verify the MCP package is available:

```bash
uvx pluglayer-mcp@latest --help
```

4. Copy this plugin into `~/plugins/pluglayer-codex-plugin`.
5. Add it to `~/.agents/plugins/marketplace.json` as a local personal-marketplace plugin.
6. Fully quit and reopen the Codex desktop app, or run `codex plugin add pluglayer-codex-plugin@personal` if you have the CLI.
7. Confirm the PlugLayer MCP server connects successfully.
8. Start with one of the prompts below.

## MCP configuration used by this plugin

```json
{
  "mcpServers": {
    "pluglayer": {
      "command": "uvx",
      "type": "stdio",
      "args": ["pluglayer-mcp@latest"]
    }
  }
}
```

## Good first prompts
- "Inspect this repo and tell me whether I should deploy it with Dockerfile or docker-compose."
- "Create a PlugLayer project for this repo and deploy it."
- "Build this repo, deploy it to PlugLayer, and use the default domain for now."
- "Set up GitHub Actions CI/CD for this already-deployed app."
- "Merge the runtime variables from this `.env` file into my existing app and restart it without showing their values."
- "Help me attach my custom domain and explain exactly what to put in my DNS provider."
- "Why did this PlugLayer deploy fail? Check logs and fix it."
- "Report this PlugLayer problem and include only safe diagnostic context."

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
- authenticated feedback submission, ticket-status checks, and owner-scoped title/description updates

For DNS-heavy flows, the plugin should translate PlugLayer's exact DNS names using the authoritative zone. Root and `www` are separate exact routes, so the plugin asks which must work and either attaches both or configures an HTTPS permanent redirect to the canonical hostname. It validates a nested path so the redirect does not drop the path or query. GoDaddy cannot publish a CNAME at `@`, so its supported apex path is a PlugLayer `www` custom domain plus GoDaddy HTTPS Permanent (301) Forward only from the root, without masking.

It does not expose PlugLayer admin-only tools. The MCP surface is focused on what an end user needs to ship and operate their own apps. Compute inventory and purchasing stay read-only, while project owners may attach/detach existing dedicated nodes through backend-guarded tools; users can remove their own apps, and project removal remains an end-user project workflow rather than an admin action.

## Troubleshooting
- If Codex desktop does not show PlugLayer after install, fully quit and reopen the app so it reloads the personal marketplace.
- If Codex cannot connect to PlugLayer MCP, rerun the installer or choose the token update option.
- If `uvx pluglayer-mcp@latest` fails, repair the published `pluglayer-mcp` package first.
- If you change `.codex-plugin/plugin.json`, `.mcp.json`, or any skill files, reload Codex so the plugin metadata refreshes.

## Marketplace templates

Use `manage-templates` to author or clone private Compose templates, preview and test them,
submit for admin review, track reviewer notes, and maintain template-backed apps.
Start with: “Turn this Compose file into a private PlugLayer template and submit it
after testing.” Public tools cannot approve or publish submissions. The matching
backend and `pluglayer-mcp` release must be deployed before these tools are usable.

## App checks and traffic protection

Ask “Check my apps” or “Check my app security” to review app status, recent logs,
exposure, and existing protections. `check-app-security` separates traffic abuse
from app faults and explains any missing telemetry. Ask “Check my apps and fix
suitable traffic-protection issues” to authorize appropriate mitigation.

Use `manage-app-access` to configure IP allowlists, HTTP rate limits, and TCP
connection caps. Existing values are preserved, changes are verified, and ingress
updates need no restart. Trusted CIDRs and public/private audience changes must
come from you; a check-only request produces findings and concrete proposals.

Examples: “Set this app's HTTP rate limit and preserve its allowlist”; “Restrict
this private app to my approved VPN CIDRs”; “Investigate these 429 errors”.
This review is not a penetration test. The matching backend and MCP release must
be available for policy updates; missing tools/routes are reported explicitly.
