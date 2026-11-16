# Issue

**Title:** feat(cli): INFO on explicit --deterministic; fix online-knob warning grammar

## Description

Answers "do we have a PR to flip the default": **the flip already merged in #1150.** `--deterministic` is the default, `--online` selects the deprecated one-pass path, and the three online-only knobs already warn-and-ignore without `--online`, naming the 2.7.0 removal. This PR closes the two gaps against your spec.

## 1. INFO on explicit `--deterministic`

`args.deterministic` was **never read** — passing the flag did nothing and said nothing. It now logs, at INFO:

```
--deterministic is the default since 2.6.0 and no longer needs to be passed;
accepting it as a no-op. Pass --online for the deprecated one-pass path
(removal planned for 2.7.0).
```

A default run (no flag) stays silent. Verified both ways.

## 2. The online-only flag set is complete — Ben's three are all of them

You asked to confirm the list. `QuantOptions` tags **exactly three** fields as online-phase, and I traced each to its sole consumer in the online EM:

| flag | field | warns without `--online`? |
|---|---|---|
| `--forgettingFactor` (`-f`) | `forgetting_factor` | ✓ |
| `--numAuxModelSamples` | `num_aux_model_samples` | ✓ |
| `--numPreAuxModelSamples` | `num_pre_aux_model_samples` | ✓ |

Everything else is both-mode or honoured by construction: `--initUniform` (the offline EM always starts uniform in reads mode; only online `-a` warm-starts), `--maxReadOcc`, `--biasSpeedSamp`, `--numGCBins`/`--conditionalGCBins`, `--vbPrior`, `--perNucleotidePrior`, `--scoreExp`, bootstrap/Gibbs. `--numBiasSamples` does not exist in this port (bias sampling is dual-phase now). **No other flag needs warn-without-online.**

## 3. Grammar fix found while verifying

The online-knob warning hard-coded the plural, so one flag read:

> `--forgettingFactor` **configure** the online inference path … to use **them**.

Now it agrees in number — "configures … to use it" for one, "configure … them" for several — the same care `warn_inert_in_mode` already takes (the #1162 item-6 class).

## Behaviour, all verified on the built binary

- explicit `--deterministic` → INFO; bare run → silent
- `-f 0.7` (no `--online`) → `configures … to use it.` naming 2.7.0
- `-f 0.7 --numAuxModelSamples 1000` → `configure … to use them.`
- `--online -f 0.7` → the knob is honoured, no inert-knob warning (and the `--online` deprecation warning fires)

Two integration tests pin all of the above. `cargo fmt`, `clippy -p salmon-cli --all-targets -D warnings`, and the `input_validation` suite (10 pass) are clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `026a85d99947`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.