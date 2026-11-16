# Issue

**Title:** fix: ci's and scanpy 1.13 plot compat

## Description

This pull request improves compatibility with recent Scanpy releases, refactors how plotting palettes are imported, and reorganizes experimental plotting tests. It also adjusts test execution in pre-release environments to avoid failures due to external dependencies.

**Scanpy compatibility and palette import refactor:**
- Improved compatibility with Scanpy 1.13+ by updating imports in `src/squidpy/_compat.py` to use the new `scanpy.plotting.legacy` module when available, including fallback logic for older versions. The `default_palette` is now also imported via `_compat.py` and re-exported for use elsewhere.
- Updated `src/squidpy/im/_container.py` to import `default_palette` from `squidpy._compat` instead of directly from Scanpy, ensuring consistent palette usage regardless of Scanpy version.

**Test organization and execution:**
- Moved the visual regression test for stain normalization from `tests/experimental/test_stain_normalize.py` to a new file, `tests/experimental/plotting/test_stain_normalize.py`, and updated imports accordingly. [[1]](diffhunk://#diff-09fbae263795e120e156d155f9ba4b1535b96bea704e2efce35eff06b76c9c4cR1-R37) [[2]](diffhunk://#diff-74ce08da45054a2aa148f15f1e1363b842ece21f3892858096b5bc0ea6d5c05fL230-L253) [[3]](diffhunk://#diff-74ce08da45054a2aa148f15f1e1363b842ece21f3892858096b5bc0ea6d5c05fL4-L8) [[4]](diffhunk://#diff-74ce08da45054a2aa148f15f1e1363b842ece21f3892858096b5bc0ea6d5c05fL21-L23)
- Modified `hatch.toml` to skip running the experimental plotting tests in pre-release environments, preventing unrelated failures due to upstream changes in `spatialdata-plot`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b71dae115e80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.