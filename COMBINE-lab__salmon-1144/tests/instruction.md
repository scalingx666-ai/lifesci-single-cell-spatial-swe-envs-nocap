# Issue

**Title:** fix(cli): forward the inference knobs --deterministic was dropping (#1140 PR A)

## Description

PR A of #1140. `run_deterministic` hand-copies the reads-mode request into the `AlignQuantOptions` the requant pass takes, and three knobs never made the trip: the flag was accepted, the run succeeded, and nothing happened.

## What was dropped

| flag | effect it should have | status before |
|---|---|---|
| `--biasSpeedSamp` | fragment-length stride of the GC effective-length convolution | forwarded nowhere; `AlignQuantOptions` default (5) used |
| `--noBiasLengthThreshold` | accept a bias-corrected effective length outright instead of flooring it at the lower barrier | same |
| `--initUniform` | start the EM from a uniform abundance vector | `QuantOptions` had no such field at all, so reads mode never carried it in either path |

`--initUniform` is now a `QuantOptions` field, per your note that the flip will want it there anyway.

## The seam, since the block was the root cause

The forwarding is now `requant_options(&map_opts, rad_path, out_dir, bias_targets) -> AlignQuantOptions`, with two unit tests: one sets every forwarded knob to a value different from its `AlignQuantOptions` default and asserts each one arrives, the other asserts an unset request leaves them at the defaults, so the first test is measuring forwarding rather than a coincidence. A field dropped from that mapping now fails a test instead of failing silently at runtime.

`ref_seqs` stays with the caller: it reads the index from disk, and only the caller knows whether bias correction asked for it.

## End-to-end, and what it can honestly show

`--biasSpeedSamp 25` with `--gcBias` under `--deterministic`, 3000-transcript fixture, 300k pairs:

```
before   quant.sf md5 57985fee3ebe9037e05071f3789efc06   (identical with and without the flag)
after    quant.sf md5 d5058db964800db47fa0146ddba4d74a   (differs from the no-flag run)
```

The other two produce no observable diff on that fixture, and I would rather say why than quietly omit them:

- `--noBiasLengthThreshold` removes a floor that only binds when a bias-corrected length falls below the uncorrected one. That never happens on this fixture, so the corrected lengths are the same either way.
- `--initUniform` changes where the EM starts, and it converges to the same optimum from either start on a well-conditioned input.

Both are forwarded and covered by the unit test. Neither absence of a diff is evidence that they are not.

## Out of scope, deliberately

`--initUniform` still does nothing in one-pass reads mode: there is no initialisation step there, since the online EM starts from the abundances it accumulated while mapping. Per your scoping this PR does not invent behaviour for a path headed for deprecation; it only stops the flag from being silently inert, with a warning naming where the flag does apply. Say the word if you would rather drop even the warning from this PR and let the flip handle it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4db6f0e3af39`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.