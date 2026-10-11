# PlugLayer installation instructions for Codex

You are installing the official PlugLayer Codex plugin. Follow this document
from top to bottom and do not substitute an MCP-only connection for the plugin.

1. Read the available package version from `plugin.json` (or `.codex-plugin/plugin.json` on legacy hosts) in the official
   repository. Inspect the installed PlugLayer package and its version.
2. Use Codex's native Plugins manager to install `pluglayer-codex-plugin` from
   `https://github.com/pluglayer/codex-plugin`, or update it when the installed
   version is older than the available version.
3. Run the package onboarding/setup action. It installs the bundled PlugLayer
   skills and the seven Codex agent definitions. Preserve user-edited agent
   files and report conflicts instead of overwriting them.
4. Confirm the package contains skills, agents, and its hosted MCP connection.
5. Use the bundled MCP connection at `https://mcp.pluglayer.com/mcp`.
6. Choose OAuth/browser authentication. Open the browser, let the user sign in
   to PlugLayer and approve access, and allow the browser callback to finish.
7. Call `get_current_user` and `list_projects` and inspect the actual results.
8. Report the installed version, loaded components, and whether PlugLayer is
   ready. If the native Plugins manager is unavailable, state that exact
   limitation and do not claim installation succeeded.

Do not install Python, uv, pip, Node, Docker, Git, a desktop installer, or a
local PlugLayer connector. Never request or print an API token in chat.

Retain a same-version or newer installation; never downgrade. Perform supported
installation, update, and connection steps yourself using available host tools
or the host's existing native CLI. Do not ask the user to type terminal commands.
Respect host permissions and request only the specific approval or UI action that
you cannot perform. A browser loopback callback is created by the host: keep its
login process running, do not invent authorization URLs or reopen expired callbacks. Never copy the localhost callback URL or authorization code into chat; the native agent must receive it automatically.
If the portal prompt specifies an MCP URL, use that environment for this setup;
otherwise use the production URL above. Do not edit a shared plugin cache to
change its environment. Report any native configuration limitation.
