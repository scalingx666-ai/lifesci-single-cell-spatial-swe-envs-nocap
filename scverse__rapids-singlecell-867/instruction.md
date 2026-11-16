# Issue

**Title:** Build rapids-singlecell once per GPU CI job and keep build and JIT caches

## Description

The GPU test jobs spend 10 of their 30 minutes compiling rapids-singlecell twice (hatch installs the project editable, then re-syncs the test group with `--editable .` again, each time in a fresh isolated build environment), and every fresh cirun VM recompiles every CuPy and numba kernel during the tests. The stable job has hit the 30 minute limit on every main run since 10-28.

- Install the build backend into the hatch env and build rapids-singlecell without build isolation in CI, so the second editable install is an incremental no-op (measured locally: 50 s → 3 s).
- Keep the scikit-build dir and the CuPy and numba JIT caches in an Actions cache per environment (about 80 MB plus a few MB).
- Measure coverage with the `sysmon` core.
- Raise the job limit to 45 minutes until the new timings are known.

CI-only change; the first run on this PR still builds from scratch and seeds the caches, the second shows the effect.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b1de455d1e9f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.