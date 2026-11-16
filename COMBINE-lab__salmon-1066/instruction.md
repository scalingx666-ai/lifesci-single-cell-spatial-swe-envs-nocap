# Issue

**Title:** fix(rad): --fldPolicy, and warn when a baked FLD makes --fldMean/--fldSD ineffective

## Description

.

## The problem

salmon's RAD writer bakes its fragment-length distribution into the header, and the reader prefers it over `--fldMean`/`--fldSD`/`--fldMax`. Preferring it is correct — it reproduces the writing run exactly — but salmon accepted those flags and then provably ignored them. A fragment-length sensitivity analysis could run to completion having perturbed nothing, every output byte-identical, with nothing in the logs or `meta_info.json` explaining why.

Thanks to @Hugo-Polloli for the report, which pinned the precedence to the exact lines in `rad.rs` and came with a clean reproducer.

## Two corrections to the report's scope

**It is broader than reported.** The comment at `rad.rs` claiming `--skipQuant` RADs derive their FLD is wrong: `salmon-quant` bakes the FLD *unconditionally* (`--skipQuant` suppresses only the baked abundances). So this affects **every salmon-written RAD**, and there was no escape hatch at all — not even the `--skipQuant` one the comment implies. Confirmed:

```
baked.rad   (full quant)  -> using fragment-length distribution baked in the RAD header
unbaked.rad (--skipQuant) -> using fragment-length distribution baked in the RAD header
```

**It is narrower in one respect.** `--fldMean`/`--fldSD` are *not* inert on a piscem RAD: `DiscreteFld::finish` seeds the derived distribution with them at weight 1, so they are a genuine (if easily dominated) prior there. That path must not warn.

I also checked the other baked header values — library format is consulted only under `-l A` (an explicit `-l` wins), and score-kind and abundances have no shadowing user flag. The FLD was the only baked value that superseded explicit user options.

## Single-end RADs are a sharper case

A single-end run has no fragment lengths to observe, so what it bakes is simply its own `--fldMean`/`--fldSD` prior. Reading such a RAD back silently inherits *the writing run's* prior as though it were empirical:

| written with | read back as |
| --- | --- |
| `--fldMean 150 --fldSD 20` | mean=150.0000 sd=20.0021 |
| `--fldMean 400 --fldSD 80` | mean=400.0001 sd=80.0002 |

The reader can detect this from the baked library format's read type — no format change needed — so it reports `frag_length_source: rad_baked_prior` and words the warning accordingly.

## What this adds

**`--fldPolicy {baked,derive,prior}`**, default `baked` — behavior unchanged.

| Policy | Behavior |
| --- | --- |
| `baked` *(default)* | Use the RAD's baked distribution. Exact parity with the writing run. |
| `derive` | Ignore it; rebuild from this RAD's own uniquely-mapped proper pairs. |
| `prior` | Ignore both; `--fldMean`/`--fldSD` alone determine it. |

`derive` and `prior` were already-implemented branches, so this mostly exposes existing paths.

**A warning, not an error**, when a baked distribution supersedes explicitly-supplied FLD flags:

```
WARN --fldMean/--fldSD had no effect: this RAD carries a baked fragment-length
distribution (mean=178.056, sd=24.076), which takes precedence. That distribution
was observed by the run that wrote the RAD. Pass `--fldPolicy prior` to use your
values instead, or `--fldPolicy derive` to re-derive the distribution from this
RAD's own fragment lengths.
```

`derive` is offered only for paired-end RADs — single-end data has nothing to re-derive from, so suggesting it would route the user back to the prior by a longer path. Detecting "explicitly supplied" means the three FLD flags become `Option` with defaults applied in `main.rs`, so a run that merely inherits them is not nagged.

**`frag_length_source` in `meta_info.json`**, across every mode, so provenance stays auditable after the fact:

```
reads       -> reads          rad baked  -> rad_baked
align -a    -> alignments     rad derive -> rad_derived
                              rad prior  -> prior
```

`--fldPolicy` warns and is ignored in reads and `-a` modes, which have no RAD header to read.

## Verification

The issue's exact reproducer now warns on both runs and reports `source=rad_baked`. Sensitivity analysis works under the new policy:

```
--fldPolicy prior --fldMean 150 -> mean=150.000 source=prior
--fldPolicy prior --fldMean 400 -> mean=400.000 source=prior
quant.sf DIFFERS
```

Tests: 4 new RAD-input tests (provenance, `derive` ignores the baked mean of ~500 in favor of the records' implied 200, `prior` puts the supplied values in control, and differing priors produce differing effective lengths only under `prior`), plus unit tests for the explicit-arg tracking and CLI parsing. `cargo test --workspace --release` — 27 test binaries, zero failures. `cargo fmt --check` clean; clippy clean on the touched crates (the three remaining `salmon-model` warnings are pre-existing on `develop`).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01R5jNNvJnFRiu2eC1JZAu2T

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6e32be98e9d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.