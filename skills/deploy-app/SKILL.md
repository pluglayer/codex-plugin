---
name: deploy-app
description: Deploy a local repo, Docker image, or docker-compose app to PlugLayer using the PlugLayer MCP tools.
---

# Deploy App to PlugLayer

Use this skill when the user wants to ship an app to PlugLayer.

## Workflow
1. Confirm the deploy unit using local repo inspection.
2. Check PlugLayer project availability.
   - If the user names a project, use it.
   - If not, choose an existing suitable project or create a new one.
3. Check compute availability with PlugLayer tools.
   - If the user is still planning and does not know how much compute they need, call `estimate_compute` first.
4. Choose placement:
   - `personal` when the user explicitly wants their own node
   - `shared` when the user explicitly wants PlugLayer shared compute
   - `auto` otherwise
5. Decide deploy type:
   - Docker image if image exists or Dockerfile-backed workflow is already prepared
   - docker-compose when multiple units need to be deployed together
6. Deploy.
7. Monitor status and tasks.
8. Return the final URL/status and next steps.

## Required checks before deploy
- project exists
- at least one ready compute path exists for the chosen placement
- port is known
- app binds in a network-safe way
- env vars are accounted for

## PlugLayer MCP actions to prefer
- list/create projects
- estimate compute when sizing is unclear
- get my available compute
- get compute summary
- list nodes
- add personal SSH node when the user needs self-managed compute
- list registries
- deploy image
- deploy compose
- get deployment/app status
- get task status
- get logs when needed

## Image deploy default
For image deployments through the PlugLayer MCP, prefer the PlugLayer-managed mirror flow by default.

- Treat a source image like `nginx:latest` or `ghcr.io/org/app:v1` as the input image.
- Check `list_registries` when the user may want or need a managed push destination.
- Let PlugLayer mirror it into a configured PlugLayer registry before deployment unless the user explicitly asks not to.
- For Docker Hub today, the mirrored destination should look like:
  - `{registry_namespace}/{USER}_{PROJECT}_{APP_NAME}:{TAG}`
- Mention the mirrored image in the final summary when available.

## Result format
Always summarize:
- deploy type used
- project
- compute placement
- app status
- public URL if any
- local fix guidance if deployment failed
