# Issue

**Title:** fix(main): clumping reports join the clump-only collision pre-flights

## Description

`--clump_only --paired -o out A/reads.fq B/reads.fq` exited 0 with ONE clumping report: primaries carry `_clumped_1`/`_clumped_2` and never collide, but reports key on the bare input filename, so R2's report silently overwrote R1's — the #388 shape on the clump path. Clumping-report paths now join the collision pre-flight on every clump arm via a shared `clump_report_candidates` helper (gated on `--no_report_file`, matching the writers), which also stops a clumping report from destroying an *input* named like one (the SE and paired-uBAM Shape A arms both did that at exit 0). `run_specialty_paired`'s namer widens to `Vec<PathBuf>` ("every path this pair writes") — pre-flight-only, so no written byte changes on accepted runs. `PAIRED_REPORT_HINT` is reworded to stop claiming directory-independence that doesn't hold. The io.rs naming property tests now cover the clump namers via `collision_key`, holding the "report collides ⇒ primary already collided" invariant in CI.

Expected-fail control: all six new rejection tests were run against the unpatched tree first and all six exited 0 there (the two alias cases destroying an input in the process); the three acceptance controls passed unpatched. Post-fix: 9/9 green, 557 total.

Plan + dual plan-review + implementation notes: `plans/08082026_clump-paired-report-preflight/` (artifacts follow in a second commit after code review + coverage audit complete).

 (manual close needed — dev is not the default branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ea274184772`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.