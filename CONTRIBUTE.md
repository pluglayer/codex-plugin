# Contributing to PlugLayer Codex Plugin

This repository contains the PlugLayer Codex plugin, MCP configuration, and Codex-oriented skills for deployment workflows.

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

## Security

- Never commit real tokens
- Keep examples public-safe
- Prefer least-privilege guidance
- Report security issues privately to maintainers

## Maintainer workflow note

This repository is synced from a private source repository. Public changes may be merged through controlled `dev -> main` flows by maintainers, so please use contributor branches and avoid direct pushes to protected branches.
