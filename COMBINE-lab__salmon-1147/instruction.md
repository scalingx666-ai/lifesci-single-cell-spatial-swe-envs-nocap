# Issue

**Title:** feat: dump equivalence classes from the RAD path, not before they exist (#1140 PR C)

## Description

PR C of #1140. `--dumpEq` under `--deterministic` wrote a well-formed `eq_classes.txt.gz` declaring **zero** classes: the mapping pass wrote it, and at that point there are none, because the classes are assembled by the quantification pass from the RAD. Nothing overwrote it afterwards, so the run produced a file whose header says `2996` transcripts and `0` classes beside a `quant.sf` derived from 4469 of them. Worse than a missing file, since nothing about it looks wrong.

## Shape, as you suggested

The serializer moves to `salmon-eqclass` as `write_eq_classes(dir, names: &[String], collapsed, with_weights)`, beside the `CollapsedEqClasses` it writes. It could not be shared before because it took a `SalmonIndex`, which the RAD path does not have; taking the names is all it needed. Both callers are now thin, and the two paths cannot drift into writing different bytes for the same classes. `flate2` as a direct dependency of `salmon-eqclass` rather than routing through `salmon-core::compress`, since the format is line-oriented text straight into a `GzEncoder`.

- `quantify_rad` dumps after collapsing, where the classes the EM consumes exist.
- `run_deterministic` takes the two flags off phase 1 and sets them on phase 2, so phase 1 also stops forcing `build_eq` to fill a builder nothing reads.
- `-a`, `--rad` and genome projection gain `--dumpEq`/`--dumpEqWeights`: same quantifier, the flags were simply never wired to it.

## Measured

Same 300k-fragment input, `--dumpEq`, before and after:

```
before   one-pass  header "2996 4468"      det  header "2996 0"      (5599 bytes of nothing)
after    one-pass  header "2996 4468"      det  header "2996 4469"
```

The one-class difference between the modes is real and not a defect of either: the fixed FLD moves a weight across the acceptance boundary. In both modes the declared count equals the number of class lines, and the per-class counts sum to the mapped-fragment total from `meta_info.json`.

## Testing

Rather than assert the two modes produce identical class sets (they do not, see above), the end-to-end test asserts the invariants that must hold in each mode: the declared count is non-zero, it equals the number of lines, the counts account for every mapped fragment, and the transcript-name block is the index's. It drives the built binary, because the bug was in how the two passes were wired rather than in the writer.

A unit test in `salmon-eqclass` pins the two output shapes: collapsed by transcript set without weights (two range-factorized sub-classes over the same set merging into one line, counts summed), verbatim with them.

## Overlap warning

This touches `run_deterministic` in `crates/salmon-cli/src/main.rs`, which #1146 rewrites substantially. The overlap is four lines (taking `dump_eq`/`dump_eq_weights` off `map_opts`, setting them on the phase-2 options), so whichever lands second is a trivial rebase. Happy to rebase this onto #1146 rather than the other way round, since yours is the larger change there. Same applies to #1144, which extracts the phase-2 option building into a named function.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4b259db18a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.