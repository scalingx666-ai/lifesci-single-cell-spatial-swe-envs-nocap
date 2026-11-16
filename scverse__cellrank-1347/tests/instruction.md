# Issue

**Title:** docs(kernels): document how to save plot_projection figures

## Description

## Description

.

`KernelExpression.plot_projection` forwards its `**kwargs` to scvelo's `velocity_embedding_stream` / `velocity_embedding_grid`, so saving a figure works exactly like in scvelo/scanpy — but this was never documented, leading to recurring "how do I save this to PDF?" confusion (and a common false-negative where scvelo's `save=` writes to `./figures/scvelo_<name>.pdf` rather than the path the user typed).

This PR clarifies the `plot_projection` docstring with both options:

- `save='<name>.pdf'` — forwarded to scvelo, which writes to `scv.settings.figdir` (default `./figures/`) with a prefix.
- `show=False` + `matplotlib.pyplot.savefig(...)` — the more reliable approach, saving wherever you want in any format.

Docs-only change; no behavior change.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b445f253241`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.