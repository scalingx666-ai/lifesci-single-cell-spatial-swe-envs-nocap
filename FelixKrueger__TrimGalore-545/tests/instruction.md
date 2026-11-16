# Issue

**Title:** fix(report): count unpaired rescues where they are written

## Description

A paired run at `--cores >= 2` without `--retain_unpaired` reported `Unpaired read 2 kept: 4` beside no unpaired file, and carried the same figure in `r1_unpaired` / `r2_unpaired` in the JSON. `classify_paired` incremented on the pair filter's `r1_ok` / `r2_ok` alone, and it is never given the writer state, so it could not know whether a rescue file had been opened. Clipping is not needed to reach it: plain `--paired` over data where one mate survives the length filter and the other does not is enough, which includes every `--clumpify` run, since `--clumpify` forces `--cores >= 2`.

With `--retain_unpaired` the figure was already right at every core count — 4 reported, 4 records on disk. So the parallel path was reporting the correct answer to a question nobody had asked.

The two increments move into the `PairOutcome::Unpaired` arm of `process_pairs`, inside the `Some(writer) && r*_ok` guards that already governed the writes. That predicate is the serial path's, and the placement after the write is Perl 0.6.11's — `++$read_1_printed` sits inside `if ($retain)` after the four `print UNPAIRED1` statements, and the report line calls the figure "printed". So this restores upstream behaviour rather than inventing a convention. `classify_paired` has one caller and `PairOutcome::Unpaired` one consumer, so no route escapes the guard; `process_paired_batch` likewise has one caller, so `--clumpify` cannot bypass it.

For runs without rescue the text block stops being emitted and the JSON values drop from a spurious count to 0. Both now match `--cores 1`.

Two tests already asserted `PairValidationStats` parity and **both were blind here**. The passthrough fixture made *both* mates short, so `r1_ok == r2_ok == false` and neither path incremented — its own comment said as much. The paired test added by #543 inherits `length_cutoff: 0`, leaving the `TooShort` arm unreachable. The new test drives four pair shapes — R2-rescued, R1-rescued, both-rescued (the #245 shape, which `src/filters.rs` makes reachable) and neither — across 4,200 pairs and both gzip modes, asserting hand-derived absolute totals rather than only serial-against-parallel. `gen_multiome_rows` now pairs its short R1 with a rescuable R2, so the passthrough test pins the no-rescue case too.

Checked against five mutants. Reverting either increment alone fails on its own side. Removing all four, serial included, makes the parity comparison **pass** at 0/0 and is caught only by the absolute anchors — which is why they are there, and why a later cleanup shouldn't soften them. Reintroducing the original bug fails two tests, which is what proves the passthrough fixture is no longer blind. The fixture totals and the batch-spanning read count are themselves `const` assertions, so a degenerate edit fails the build rather than passing silently.

845 tests, `clippy --all-targets --release -D warnings` clean, `fmt --check` clean. Verified end to end: no `Unpaired read` block at `--cores 1` or `4` without rescue, with and without clipping; `read 2 kept: 4` and a 4-record file at both core counts with it; JSON keys present at 0 throughout; trimmed records byte-identical to pre-fix. Note the CI validation matrix runs `--cores 1`, so it exercises the already-correct path and proves no collateral damage rather than the fix.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `86aa3012dedb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.