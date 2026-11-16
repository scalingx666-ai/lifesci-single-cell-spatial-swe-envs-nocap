# Issue

**Title:** ci(synbio): gate the [synbio] extra, and make its two scripts real tests

## Description

. That PR fixed an extra that had been uninstallable since #887; this one adds the gate that should have caught it on day one.

## Why nothing caught it

Two independent holes:

1. **No workflow ever installs it.** `python-package.yml` installs `.[tests,mcp]` — `synbio` is never touched, so `pip install "omicverse[synbio]"` was never once executed in CI.
2. **The module's own verification scripts were invisible to pytest.** `tests/synbio_coupling_demo.py` and `tests/synbio_gpu_smoke.py` are not named `test_*.py`, and `[tool.pytest.ini_options] python_files = ["test_*.py"]`. They were never collected — 86 public APIs with zero automated coverage.

## `.github/workflows/synbio.yml`

Split by cost. Both timings measured in a clean `python:3.11` x86_64 container against this pyproject:

| job | cost | what it proves |
|---|---|---|
| `resolve` (matrix 3.10/3.11/3.12) | **11s**, 203 packages | the extra is satisfiable at all |
| `install` | **137s**, 6.1 GB on disk | the resolved set installs, and layer A really solves |

**The gate is verified against the actual bug, not assumed.** Re-injecting `rs3>=0.0.18` into the extra and running the exact command CI runs:

| Python | result |
|---|---|
| 3.10 / 3.11 / 3.12 | all three exit non-zero — gate goes red |

On failure it emits a `::error::` explaining that one bad pin makes the *entire* extra uninstallable (not just that package), and points at `_rs3.py`'s `--no-deps` runtime fetch as the escape hatch for genuinely unresolvable dependencies.

`resolve` alone would have caught rs3, in 11 seconds, three years' worth of PRs ago.

## The two scripts become real tests

They gate themselves **at runtime**, not via `-m` filters — `conftest.py` registers `requires_gpu` / `requires_network` markers but attaches no skip logic to them, and CI runs a bare `pytest`. A marker alone would have let the GPU suite try to pull several GB of checkpoints onto a CPU runner.

- **`test_synbio_coupling.py`** — `importorskip("cobra")`. Splits the demo so layer A is testable without the protein stack: use a fixed kcat, then assert that under one shared protein budget a slower enzyme cannot out-grow a faster one — and that `slower < faster` *strictly*. If those come out equal the enzyme constraint is not binding and the A↔B hinge is decorative. The full kcat→flux hinge stays as its own test, skipping if DLKcat is unavailable.
- **`test_synbio_gpu.py`** — `importorskip("torch")` + `skipif(not cuda)`. Asserts `enzyme_kcat` actually moves when the sequence changes; identical kcat for two different sequences would mean the model never read the sequence at all.

## Verification

Full container run of the `install` job, step by step:

```
install OK
### step 1: Layer-A smoke
  test_fba_solves_wild_type_growth PASSED
  test_ec_model_constrains_growth_and_respects_the_protein_budget PASSED
  test_full_kcat_to_flux_hinge PASSED
  3 passed in 246.87s
### step 2: CRISPR + extra guards      -> 4 passed
### step 3: GPU suite must SKIP        -> 6 skipped
```

The full DLKcat hinge passed too, so the moat feature is exercised end to end.

That run also caught a wrong comment of mine: I had written that `e_coli_core` "ships with cobrapy, no network", but the container showed it downloading ~35 kB from BiGG. Those tests are now marked `requires_network` and say so.

## Note

`install` needs ~6.1 GB (pytorch-lightning pulls torch). That fits a standard `ubuntu-latest` runner, but it is worth knowing before adding more to the extra.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60648ae6371f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.