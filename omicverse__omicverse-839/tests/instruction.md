# Issue

**Title:** fix(registry): hydrate full registry on first lookup

## Description

## Problem

`ov.utils.registry_lookup(...)` only ever returned a handful of functions instead of the full registry. Immune-repertoire (`ov.airr.*`), QC, and many other functions were effectively invisible to the lookup helper (and to any external agent harness that calls it).

## Root cause

`RegistryScanner.ensure_runtime_registry()` skipped the full module hydration pass whenever `_global_registry._registry` was non-empty:

```python
if getattr(_global_registry, "_registry", None):
    return
```

The registry is populated lazily through `@register_function` import side effects. A plain `import omicverse as ov` already registers a small number of functions from eagerly-imported submodules, so that **non-empty-but-partial** dict satisfied the truthiness guard and hydration was permanently skipped. Lookups then only saw those few stub functions.

## Fix

- Add an idempotent `FunctionRegistry._ensure_hydrated()` memo, guarded by a `_hydrated` flag that is set **before** hydrating (to avoid re-entrancy if a submodule import triggers another query), and call it at the top of `find()` so the direct `find`/`find_function` path benefits too.
- Gate `ensure_runtime_registry()` on that `_hydrated` memo instead of on registry emptiness, with a fallback to `_hydrate_registry_for_export()` for older registry objects.

No behavior change for `export_registry()` / `ov.Agent` — they already hydrated; this only fixes the lookup path that was short-circuiting.

## Verification

```
import omicverse as ov         -> registry size 0,    _hydrated False
first registry_lookup(...)     -> registry size 7604, _hydrated True
```

- `registry_lookup('immune repertoire TCR BCR clonotype airr')` now returns real `ov.airr.meta_clonotypes(...)` results with full docstrings.
- `registry_lookup('quality control doublet mitochondria filter cells')` returns 10 matches.
- Idempotent: the `_hydrated` memo + scanner cache mean subsequent calls pay no extra hydration cost.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `763967cd7242`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.