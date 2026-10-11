# PlugLayer Codex Plugin

PlugLayer gives Codex a direct path from source to a live service on compute
dedicated to your project. The [PlugLayer landing page](https://pluglayer.com)
shows the same flow through its 3D scenes: a platform hub connects source,
app, database, and domain; a compute-fabric field shows placement and capacity;
a rotating database tower represents engines that arrive already wired; and the
marketplace mascot represents ready-to-run apps and tools.

## What it can do

From a plain-English request, the plugin can:

- inspect a repository, Dockerfile, Compose stack, or existing image and explain
  the safest deploy path, including ports, environment, storage, and capacity;
- plan and deploy apps, Compose services, marketplace templates, and databases
  such as Postgres, Mongo, Redis, and Qdrant on dedicated PlugLayer compute;
- connect apps to databases, attach persistent storage, configure project
  metadata and environment variables, and set up verified custom domains;
- read task status, logs, health, usage, and rollout state, then diagnose and
  repair failed deployments with the same backend-owned controls as the portal;
- generate CI/CD workflows, check app security and traffic controls, and share
  redacted product feedback when PlugLayer causes a problem.

The hosted MCP connection keeps Codex's actions aligned with the portal's
permissions and safeguards. Local source and Docker work uses Codex's own
capabilities. No Python, uv, Node, Docker, Git, terminal command, or PlugLayer
desktop app is required for setup.

Explore the product surfaces on the landing page: [platform](https://pluglayer.com/platform),
[dedicated compute](https://pluglayer.com/compute), [databases](https://pluglayer.com/data-layer),
[marketplace](https://pluglayer.com/templates), and [agent setup](https://pluglayer.com/agents).

## Setup

1. Open **Setup** in the PlugLayer portal.
2. Choose Codex and copy the prompt.
3. Paste it into Codex.
4. When Codex opens the browser, sign in to PlugLayer and approve OAuth.

The root `plugin.json` and `mcp.json` are the portable package entrypoints. The legacy `.codex-plugin/` manifest remains for older Codex clients. The plugin uses `https://mcp.pluglayer.com/mcp` with OAuth. Tokens are issued and refreshed by PlugLayer and remain in Codex's secure connection storage; no API token is pasted into chat.

The plugin includes PlugLayer MCP plus skills for repo inspection, deployment,
domains, CI/CD, project metadata, environment updates, feedback, security, and
deployment repair.

Detailed agent setup: [installation instructions](installation_instruction.md).
