# Issue

**Title:** fix: emit warnings that were silently discarded

## Description

### Problem

Several places in the codebase construct a `Warning(...)` object as a **bare
statement**:

```python
if param is not None:
    Warning(  # <-- constructs a Warning and throws it away; nothing is shown
        f"Using {param} after custom Dataloader was initialize is redundant, ..."
    )
```

Instantiating a `Warning` (or any subclass) does nothing on its own — the object
is immediately discarded, so the intended user-facing warning **never fires**.
The author clearly meant `warnings.warn(...)`. This affects, among others:

- redundant `indices`/`batch_size`/`n_samples` passed alongside a custom
  dataloader (`RNASeqMixin`, `VAEMixin`, `SemisupervisedTrainingMixin`, `MRVI`),
- `SemisupervisedTrainingMixin.get_ranked_features` called without an
  attributions matrix ("Missing Attributions matrix"),
- the SCANVI custom-dataloader sampler notice,
- legacy GIMVI loading when no saved AnnData is found,
- `TrainingPlan` extra-metric shape / module-training-state notices.

### Fix

Replace every bare `Warning(...)` statement (20 of them across 6 files) with a
proper `warnings.warn(msg, UserWarning, stacklevel=settings.warnings_stacklevel)`
call, matching the convention already used throughout the codebase. Behavior is
otherwise unchanged — the only difference is that the warnings are now actually
emitted. (I also dropped a redundant `"Warning: "` prefix from one message.)

### Tests

Adds `tests/test_warnings.py`:

1. `test_no_bare_warning_statements` — an AST scan asserting no `*Warning(...)`
   statement is used as a no-op anywhere in `scvi`. Fails before this change
   (20 offenders), passes after, and guards against reintroduction.
2. `test_get_ranked_features_warns_on_missing_attrs` — a behavioral test that
   `SCANVI.get_ranked_features()` (no attributions) now emits the warning.

Both tests fail on `main` and pass with this change. Existing model/train
suites (SCANVI, GIMVI, MRVI, SCVI) still pass locally.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88b4b41216ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.