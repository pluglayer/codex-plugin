---
name: setup
description: Complete or repair PlugLayer plugin setup, activate its bundled local Codex agents, and verify the hosted OAuth connection after installation or upgrade.
---

# PlugLayer setup

Use the installed plugin as the source. Locate its root from this skill's path;
read `plugin.json` and the seven `agents/pluglayer-*.toml` files. Do not download
instructions from an unverified third-party source or install a local MCP runtime.

## Local Codex agents

For local Codex, install the bundled TOML definitions into the active Codex home's
`agents/` directory (`~/.codex/agents/` by default). Use the host's file tools or
built-in OS file operations; do not require Python, Node, Git, or another runtime.
Do not edit `config.toml` or override model, sandbox, permissions, or credentials.

Keep last-installed copies of managed definitions and their package version under
`~/.pluglayer/plugin-state/codex/`. For each bundled agent:

- If the target does not exist, copy the bundled file and save its managed copy.
- If the target already equals the bundled file, retain it and record the copy.
- On upgrade, replace it only if it still equals its last-installed managed copy.
- If it differs and has no matching managed copy, preserve the user's file and
  report the exact conflict. Do not mark that agent installed or silently overwrite it.

Read back every written file and compare it to the bundled definition before
updating its managed copy. Report the installed package version and agent names.
File presence proves installation, not runtime loading: inspect the host's agent
inventory when available. If the current session has not reloaded the definitions,
tell the user that a new session is needed and report activation as pending.
Never spawn an agent or perform a deployment merely to prove setup.

Cloud ChatGPT cannot register local Codex TOML agents. Its PlugLayer workflows
use the bundled skills; do not claim that named custom agents were activated there.

## Hosted OAuth

Verify the plugin's bundled remote MCP endpoint. Use the host's native OAuth
connection flow and let the user complete browser approval. The host owns token
storage and refresh; never fetch, print, or copy credentials into prompts or files.
Use `get_current_user` and `list_projects` as read-only connection checks. Inspect
their results for authentication/tool errors before reporting success.

Report package, agents, and MCP authentication separately. If any required
component is missing, unavailable, or pending reload, report that state rather
than declaring the complete plugin ready.
