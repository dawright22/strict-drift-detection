# strict-drift-detection

A companion plugin for [Git-Ape](https://github.com/Azure/git-ape) that adds **deep, baseline-based recursive drift detection**.

Git-Ape's built-in `azure-drift-detector` skill checks a small, hardcoded list of properties per resource type against `requirements.json`. This plugin instead:

- Captures a full baseline snapshot of each resource's actual Azure state (`az resource show`)
- Recursively diffs **every** nested property on every subsequent check — not a curated subset
- Normalizes arrays (re-keys by `name`/`id`/`key`) so reordering doesn't cause false positives
- Classifies severity via an external, extensible `drift-rules.json` instead of inline bash logic
- Filters out volatile/computed noise (etags, timestamps, endpoints) via `ignore-properties.json`

See [`skills/strict-drift-detection/SKILL.md`](skills/strict-drift-detection/SKILL.md) for full usage.

## Install

```bash
copilot plugin marketplace add dawright22/strict-drift-detection
copilot plugin install strict-drift-detection@strict-drift-detection
```

## Requires

- `git-ape` plugin (>=0.3.0) — provides `.azure/deployments/<id>/metadata.json`
- Azure CLI (`az`) >= 2.58.0
- `jq` >= 1.6

## License

MIT
