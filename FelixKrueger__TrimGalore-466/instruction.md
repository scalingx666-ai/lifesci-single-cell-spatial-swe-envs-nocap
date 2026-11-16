# Issue

**Title:** fix(cli): stop --gzip's notice promising gzipped output for plain input

## Description

Addresses one of the three false strings in #453. **Does not close it** — the flag question is settled the other way (the refusal stays, per the issue) and the two banner strings are fixed in #468.

`--gzip` printed "Output is gzipped by default" on every run, but output compression follows the input (`gzip = !dont_gzip && is_gzipped(input[0])`). On a plain-text input the notice asserted something the run then did not do — and no flag makes it true, so "use `--dont_gzip` to disable" described a state already in effect. The notice is now chosen by the same fact the run uses.

<details>
<summary>Detail (AI-assisted)</summary>

Plain input now reads:

```
WARNING: --gzip is deprecated in Trim Galore v2.0. Output compression follows the input,
         so this plain-text input produces plain-text output and no flag changes that. Ignoring.
```

Gzipped input keeps the original wording verbatim.

The message deliberately offers no remedy, because there isn't one — nothing makes a plain input produce gzipped output. An earlier draft suggested "use a gzipped input, or `--dont_gzip` to be explicit" and I dropped it rather than point at a non-fix.

`io::is_gzipped` is filename-based with no filesystem access, so it is safe to call from `Cli::validate()`, and it sits after the input-existence checks in any case.

Both arms are asserted in one test, each also asserting the *absence* of the other's wording, so neither can silently drift into the other. Forcing the gzipped branch unconditionally turns that test red. 803 tests (1 new), `fmt` and `clippy --all-targets --release -D warnings` clean.

**History note:** this branch carries an add-then-revert pair. It briefly removed the `--clumpify --dont_gzip` refusal before that question was settled in the other direction; the revert restores the refusal, its unit test and the `clumpy.md` wording exactly. The net diff is the notice fix alone — `src/cli.rs`, one test, one CHANGELOG line — and the squash will flatten the history.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e86e2afbe5e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.