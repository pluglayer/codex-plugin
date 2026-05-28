# Contributing to PlugLayer Codex Plugin

This repository contains the PlugLayer Codex plugin, MCP configuration, and Codex-oriented skills for deployment workflows.

## Step-by-step contribution flow

1. Star the repository if you want to follow updates.
2. Open an issue first if the change is large or changes plugin behavior.
3. Fork the repository to your own GitHub account.
4. Clone your fork locally.
5. Create a feature branch from your fork's `dev` branch if it exists. Otherwise branch from `main`.
6. Keep the work scoped to one clear improvement.
7. Validate plugin JSON and review skill examples before pushing.
8. Push your branch to your fork.
9. Open a pull request from your fork branch into the public `dev` branch.
10. Address review feedback in the same branch.
11. Maintainers will review and promote accepted changes through the normal maintainer flow.

## Before you start

- Read `README.md`
- Keep pull requests small and intentional
- Discuss larger skill or plugin-manifest changes before implementing them

## Good contribution areas

- Better Codex skill prompts
- Clearer deployment and recovery guidance
- Safer MCP examples
- Plugin metadata cleanup
- Documentation and onboarding polish

## Avoid in this repo

- Secrets
- Internal-only instructions
- Breaking plugin manifest changes without migration notes
- Broad MCP tool changes that belong in `pluglayer-mcp` instead

## Local validation

Before opening a PR, validate plugin JSON and docs:

```bash
python - <<'PY'
import json
print(json.load(open('.mcp.json')))
print(json.load(open('.codex-plugin/plugin.json')))
PY
```

Review the skill files to make sure examples still match the current MCP tool surface.

## PR expectations

- Explain the user problem being improved
- Describe the expected Codex-side behavior
- Mention any setup or manifest changes
- Include test or manual validation notes
- Target the public `dev` branch unless a maintainer explicitly asks for another base branch

## Security

- Never commit real tokens
- Keep examples public-safe
- Prefer least-privilege guidance
- Report security issues privately to maintainers

## Maintainer workflow note

This repository is synced from a private source repository. Public changes may be merged through controlled `dev -> main` flows by maintainers, so please use contributor branches and avoid direct pushes to protected branches.
