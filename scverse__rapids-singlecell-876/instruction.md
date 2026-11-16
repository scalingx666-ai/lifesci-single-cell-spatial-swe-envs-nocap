# Issue

**Title:** Deprecate tl.louvain in favor of tl.leiden

## Description

Scanpy deprecated `tl.louvain` in favor of `tl.leiden` in 1.12 (). This does the same for `rapids_singlecell.tl.louvain`.

- `tl.louvain` gets scverse-misc's `@deprecated`, like `rank_genes_groups_logreg` and `calculate_niche`. Calling it emits a `FutureWarning` that points to `tl.leiden`, and the docs get the deprecation notice from the `scverse_misc` Sphinx extension. Behavior is unchanged, so existing code keeps working until the function is removed.
- `rsc.tl` moves `louvain` from `__all__` to `__deprecated_exports__`, which keeps it out of the live API contract the agent skill reads. `api_notes.toml` drops its entry and the `related` links to it, because `python -m rapids_singlecell_skills.api validate` rejects notes for symbols outside the live API.
- `tl.louvain` leaves the API docs. The docs build runs `sphinx-build -W` with nitpicky references, so the `{func}` roles that pointed at its page become plain code in the out-of-core page and in the 0.9.1, 0.9.4, 0.9.5, 0.9.6, 0.16.0 and 0.19.0 release notes. The out-of-core page marks it deprecated, and the release note goes under 0.19.0.

**Tests**
- New `test_louvain_deprecated` checks the `FutureWarning`, that its message points to `tl.leiden`, and that it is attributed to the caller (a decorator stacked above `@deprecated` would shift that).
- The other louvain tests in `tests/test_clustering.py` and `tests/dask/test_dask_clustering.py` ignore the new warning with a module-level `filterwarnings` mark.
- 1 GPU (GB10): `tests/test_clustering.py` 22 passed, also with `-W error::FutureWarning`; `tests/test_install_skills.py` 27 passed; `python -m rapids_singlecell_skills.api validate` passes, and rejects the old `api_notes.toml` once `louvain` leaves `__all__`.
- `tests/dask/test_dask_clustering.py` only gains the same module-level mark. Its session `LocalCUDACluster` fixture did not come up on this single-GPU box, neither within the default 60 s test timeout nor within 420 s (the `leiden` cases error the same way), so it is not covered by the runs above.
- `ruff`, `codespell` and the repo's prek hooks, `mypy` included, pass.

**LLM usage**

- [x] LLM or coding agent used: Claude Sonnet 5.5 via Claude Code
- [ ] I, a human, have reviewed, understood and tested every changed line

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `789a251daf8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.