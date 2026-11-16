# Issue

**Title:** Convert remaining generics to PEP 695 syntax

## Description

Stacked on #1221. Removes the `UP046`/`UP047` ruff ignore added there by converting the three remaining `Generic[...]` / `TypeVar`-signature definitions to PEP 695 inline type parameters.

**No behaviour or public-API change** - type parameters are erased at runtime, and every exported name is preserved.

## Changes
- `gr/neighbors.py`: `class GraphBuilder(ABC, Generic[CoordT, GraphMatrixT])` -> `class GraphBuilder[CoordT, GraphMatrixT](ABC)`. Drops the private, now-unused `CoordT` TypeVar. The module-level `GraphMatrixT` TypeVar **stays** - it backs the public `GraphPostprocessor` alias and is itself exported (`squidpy.gr.GraphMatrixT`).
- `gr/_build.py`: `class SpatialNeighborsResult(NamedTuple, Generic[GraphMatrixT])` -> `class SpatialNeighborsResult[GraphMatrixT](NamedTuple)`. The imported `GraphMatrixT` stays (re-exported via `__all__`).
- `experimental/utils/_params.py`: `resolve_params` -> `def resolve_params[T](...)`; drops the module `_T` TypeVar.
- `pyproject.toml`: removes the `UP046`/`UP047` ignore.

## Deliberately not done (would change behaviour)
- Dropping `GraphMatrixT` from `__all__` (breaking import change).
- Converting `GraphPostprocessor` to a `type` alias (changes its runtime type).

## Verification
- `ruff check .` clean with UP046/UP047 active; pre-commit clean.
- Public exports unchanged (diff vs base is only the two `Generic` import removals).
- `tests/graph/test_spatial_neighbors.py` + `tests/experimental/test_tiling_stitch.py`: 65 passed on 3.13.
- PEP 695 generic `NamedTuple`/class/function verified on a real **3.12** interpreter (the new floor) - construct/unpack/`_fields`/subscription all behave identically.

Rebase onto `main` once #1221 merges.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `821a370f93f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.