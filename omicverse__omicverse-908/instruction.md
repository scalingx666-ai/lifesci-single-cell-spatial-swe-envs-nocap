# Issue

**Title:** fix(registry): make ov.tl / ov.es / ov.micro discoverable in a fresh session

## Description

## Problem

`ov.find_function` drives registry discovery through `_hydrate_registry_for_export()`, which force-imports modules so their `@register_function` decorators run. That function's module list is **hand-maintained and had drifted from `_LAZY_MODULES`** (26 lazy modules vs 17 hydrated entries), so several modules stayed invisible to a fresh session until unrelated code happened to import them.

This is not import-chain luck: `ov.protein` works cold because it is explicitly in the list *and* has an explicit `_hydrate_registry()` hook. `ov.flow` (on `feat/ov-flow`, #907) works for nobody because it was added to `_LAZY_MODULES` and never to this list.

It matters because the registry is how omicOS agents reach functions by natural-language query — a cold session silently returns "No matching functions found" for functions that exist.

## Measured impact

Cold registry vs. fully-forced registry, two clean processes, Python 3.11:

| module | entries unreachable cold |
|---|---|
| `micro` | 53 |
| `es` | 14 |
| `tl` | 1 |

**68 of 1479 entries** invisible in a fresh session. `mcp`, `epi`, `report`, `agent` are in `_LAZY_MODULES` but carry no net registrations today — they will break the same way the moment someone adds a decorator.

## Fix

Purely additive, 28 lines, no existing code path modified:

- `_registry.py` — add `tl` / `es` / `micro` to the existing `module_names` tuple. `flow` is listed too; the import loop already tolerates a missing module, so it becomes discoverable the moment #907 merges.
- `micro/__init__.py` — add the same `_hydrate_registry()` hook that `metabol` / `protein` / `genetics` / `airr` / `mol` / `synbio` already have. `ov.micro`'s `__init__` is lazy and never imports its decorated submodules.

## Cost — measured before and after

```
import omicverse        0.17 s  ->  0.19 s     (unchanged; still fully lazy)
first find_function()   12.8-15.4 s -> 14.9-16.8 s
```

`import omicverse` is untouched — this deliberately does **not** move anything out of `_LAZY_MODULES`, which would have put 1.3-7.5 s per module onto every user's import. The added first-query cost is milder than per-module timings suggest because `tl`/`es`/`micro` share dependencies already pulled in by the modules being hydrated.

## Verification

- `rarefy`, `alpha diversity`, `cross_species_align`, `gsva` all resolve cold
- no previously-visible entry lost (diffed cold registries before/after)
- `tests/utils/registry` — 9 passed

## Deliberately out of scope

- **`ov.external` (104 entries) and `ov.llm` (9 entries) are not hydrated**, by request. They remain invisible cold — agents querying PyWGCNA / cNMF / GraphST / SCLLMManager will still miss in a fresh session.
- `_ensure_hydrated()` sets `self._hydrated = True` *before* hydrating and swallows every exception, so a partial failure permanently pins the process to a partial registry with no warning. Left untouched here; worth a separate look.
- A build-time AST index would remove the hand-maintained list entirely and cut first-query latency to ~0.02 s (prototype: 866 decorator sites scanned in 1.5 s, 3.1 MB index, 0.020 s load). It requires lazy resolution of `entry['function']` at four call sites, so it belongs in its own PR.

Separate from #907 as requested — this affects many modules, not just `flow`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97728b50f3f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.