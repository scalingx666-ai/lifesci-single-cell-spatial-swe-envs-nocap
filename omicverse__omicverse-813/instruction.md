# Issue

**Title:** fix(_monitor): surface a FAILED summary when the wrapped function raises

## Description

## Problem

`@monitor` wraps every decorated `ov` function. Its wrapper used `try/finally`, so `StructureWatcher.finish()` printed the normal green **SUMMARY** box even when the wrapped function **raised**. A failed call looked identical to a `0.0s` no-op — same box, just `Shape (Unchanged)`.

Concretely: on a machine where an optional backend dependency is missing, `ov.single.batch_correction(..., methods='harmony')` fails at `import torch` inside `omicverse.external.harmony`. Because the import error aborts in <1ms, the box reports `Duration: 0.0009s … (Unchanged)` and **no** `X_pca_harmony` is written — but nothing signals that an exception occurred. Callers that only capture stdout never see the `ModuleNotFoundError`, so a hard failure is indistinguishable from a silent no-op.

## Fix

- Capture the in-flight exception via `sys.exc_info()` in the `monitor` wrapper and pass it to `finish(error=...)`.
- New `finish(error=None)` renders a red **`[FAILED]`** box that embeds the exception type + message (word-wrapped, capped) instead of a success-styled box.
- The exception is **re-raised unchanged** — never swallowed. `finish()` is itself guarded so monitoring can never mask the real error.

## Behaviour

Before (failure looked like success):
```
╭─ SUMMARY: batch_correction ──────────────────╮
│  Duration: 0.0009s                           │
│  Shape:    93,190 x 2,000 (Unchanged)        │
│  CHANGES DETECTED                            │
╰──────────────────────────────────────────────╯
```
After:
```
╭─ SUMMARY: batch_correction [FAILED] ─────────╮
│  Duration: 0.0012s                           │
│  Status:   ✖ raised ModuleNotFoundError      │
│                                              │
│  ERROR                                       │
│  ─────                                       │
│  No module named 'torch'                     │
╰──────────────────────────────────────────────╯
```

## Safety

- Exception still propagates to the caller (verified: re-raises `ModuleNotFoundError`).
- Success path, output, and `_log_to_uns` are unchanged.
- Nesting unchanged: only the top-level call prints (same guard as the success box).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5f2b1f2870f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.