# Issue

**Title:** Fix undeclared dependencies that break `import topo`

## Description

## The bug

`import topo` fails on a clean install of topometry 1.1.0 from PyPI:

```
ModuleNotFoundError: No module named 'adjustText'
  File ".../topo/single_cell.py", line 22, in <module>
    from adjustText import adjust_text
```

`adjustText` was imported at module scope but never declared. Reproduced in a clean
Python 3.12 venv with `pip install topometry==1.1.0 scanpy`. It surfaces whenever
scanpy is present, since that is what causes `topo/__init__` to import `single_cell`.

## The fix

**`adjustText` → lazy import.** `adjust_text` is used in exactly one place —
`repel_annotation_labels()` — purely to place plot labels. Making it a hard dependency
for every user to support one figure helper is the wrong trade, so it is now imported
inside that function with a clear error message. This follows the convention the module
already uses for `scanpy`, `bbknn`, `harmonypy` and `pacmap`, and matches the file's
own stated intent about not forcing single-cell dependencies on everyone.

**`joblib` → declared.** An AST audit of every import in the package (32 modules,
subtracting stdlib and declared deps) found one other unguarded undeclared import:
`from joblib import cpu_count` at module scope in `topo/base/ann.py`, which
`topo/__init__` imports *unconditionally*. It works today only because scikit-learn
pulls joblib in transitively — an accident that breaks the day sklearn drops it. Now
declared explicitly.

The other 18 undeclared third-party imports (`hnswlib`, `pymde`, `pacmap`, `umap`,
`torch`, `faiss`, `nmslib`, `annoy`, `trimap`, `ncvis`, `MulticoreTSNE`, `pygsp`,
`pyamg`, `bbknn`, `harmonypy`, `imageio`, `PIL`, `scanpy`) are all correctly lazy or
try-guarded and need no manifest change.

Note: `setup.cfg` is the authoritative manifest here — `pyproject.toml` carries only a
`[build-system]` table, no `[project]` section.

## Verification

- Reproduced the failure against released 1.1.0 in a clean venv.
- Built sdist + wheel; installed the wheel into a fresh `/usr/bin/python3.12` venv with
  scanpy and **no manual extras** → `import topo` succeeds, and `adjustText` is confirmed
  absent from the venv.
- `adjustText` is not imported at import time; calling `repel_annotation_labels()`
  without it raises `ImportError: Label repulsion requires 'adjustText' (pip install adjustText)`.
  With it installed, the function still works.
- Test suite: **25 passed**, identical to pristine master.

## Follow-ups not in this PR

1. **Version drift.** `setup.cfg` says `version = 1.0.2` while `topo/version.py` says
   `1.1.0`, so this tree builds artifacts labelled 1.0.2. Left alone since it changes
   release semantics.
2. **`repel_annotation_labels` passes removed adjustText parameters.** Six of the eight
   kwargs it sends (`autoalign`, `expand_points`, `expand_text`, `force_points`, `lim`,
   `add_objects`) were removed in adjustText 1.0 and are now silently swallowed by
   `**kwargs`. Notably `add_objects` became `objects`, so label-vs-points avoidance is
   silently inactive on adjustText ≥ 1.0. Behavioural, not packaging — reported separately.
3. **Test dependencies undeclared.** The suite needs `scikit-misc` and `hnswlib`; without
   them 12 fail / 11 error. `scikit-misc` in particular is required by scanpy's
   `seurat_v3` HVG flavor, which is topometry's *default*.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2653faf97b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.