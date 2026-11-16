# Issue

**Title:** Add dyn.pd.plot_lap for grouped least-action path visualization

## Description

## Summary

The protocol LAP notebook defines `plot_lap` locally, so the corresponding `dyn.pd.plot_lap` call is currently unavailable. This adds a public helper for plotting selected groups from `compute_cell_type_transitions` over a velocity streamline background.

```python
fig, ax = dyn.pd.plot_lap(
    adata, transition_graph, develope_keys, title="Developmental LAPs"
)
```

The API receives the AnnData object and transition graph explicitly, returns `(fig, ax)`, and preserves the notebook's per-trajectory action coloring and short coordinate axes. It validates missing or inconsistent path data before drawing and avoids duplicate background axis annotations. API documentation and the changelog include the new helper and examples for all three path groups.

Notebook reference: https://colab.research.google.com/drive/1_EYm0f3MuPQyghiNhbEAwolIqOSAKuWE

## Validation

- `pytest tests/test_plot_lap.py tests/test_config.py tests/test_logger.py -q`: **14 passed, 3 skipped** (the skips are existing logger tests).
- Eight new offline tests cover selected path coordinates/action colors, multiple paths, an existing axes and alternate basis, malformed results, and actual streamline rendering/file output.
- Black check, targeted fatal-error Flake8 check, and `git diff --check` passed.
- Sphinx HTML build completed with repository documentation warnings; the new API page was generated.
- Visually inspected the synthetic streamline/LAP output. Full biological analyses and the complete test suite were not rerun.

The one-argument manuscript form still needs explicit `adata` and `transition_graph` arguments; the helper does not infer notebook globals.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69ba903000a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.