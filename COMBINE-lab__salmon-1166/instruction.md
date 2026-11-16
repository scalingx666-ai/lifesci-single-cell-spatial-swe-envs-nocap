# Issue

**Title:** fix(groups 4+5): metadata that tells the truth, and errors that arrive in time

## Description

**Groups 4 and 5** (#1140, #1162). You asked me to parallelize these — five agents staged disjoint files simultaneously, and I assembled and verified the result. Because the work interleaves in the same files (`main.rs` carries both groups), it lands as one PR rather than two, sectioned by group below. Stacked on #1165.

## Group 4 — metadata asserting something the run did not do

| Field | Was | Now |
|---|---|---|
| `library_types` | Reported what the **detector observed**: `-l ISR` on ISF data said `["ISF"]`, contradicting `cmd_info.json` and `lib_format_counts.json` in the same directory, on a run that really did filter as ISR and mapped **0** fragments | Reports the **applied** format. Per your call the metadata reports **both** — applied in `library_types`, inferred in `detected_library_type` |
| `num_decoy_targets` | Hardcoded `0` while `num_decoy_fragments` beside it was real, with `meta_info_complete: true` | The real count, derived from the same row split as `quant.sf` so it cannot contradict `num_valid_targets` |
| `frag_length_source` | `rad_baked` for a plain `-a` run — naming an internal intermediate the user never asked for | `alignments` for alignment input; genuine `--rad` keeps `rad_baked`, where it is correct |
| `logs/salmon_quant.log` | Labelled a default reads run "alignment mode", dropped the documented mapping-type/rate lines, and called unmapped fragments "strand-incompatible" on a run with `num_incompatible_fragments = 0` | Describes the mode the user chose |
| `num_bias_bins` | `0` | **Still `0`, now with the reason recorded** |

The `frag_length_source` fix needed a real signal rather than path-sniffing, so `AlignQuantOptions` gained `input_is_alignments`, set by the two alignment drivers.

On `num_bias_bins` — two agents independently traced it to C++'s `readBias(FORWARD).counts.size()`, the legacy fixed 4096-bin k-mer histogram behind `observed_bias.gz` that this port replaced. The GC and positional bin counts *are* in scope at the write site, but filling either in would hand a C++-schema reader a different model's number in the wrong unit. Left alone deliberately.

## Group 5 — errors that arrived too late or named the wrong flag

- **`-a` + bias without `-t` read the entire BAM before failing** — hours on real data — with a message hard-coded to say `--rad` for an invocation containing no `--rad`. Now fails at invocation (**0.00 s**), naming `-a`, the bias flags actually passed, and `-t`.
  Genome projection is deliberately **excluded**: it reconstructs reference sequences from `--genome` plus the annotation, so a blanket gate would have broken a working invocation. That catch came from the agent pushing back on my brief.
- **`quantify_rad`'s backstop message no longer asserts which input flag you typed.** It serves four user-facing modes; it now names the requirement, not the mode. Its module docs say so too, since that premise is why the bug existed.
- **FASTQ parse errors name the file.** With several files the message states the list is the *candidate set* rather than claiming a culprit — the pinned paraseq discards reader identity before the error surfaces, so naming the exact file needs an upstream change. Recorded in #1162.
- `-2` without `-1` says what is missing instead of "no reads provided".
- The `--decoyThreshold`/`--sketch` warning moved inside reads dispatch; it used to fire in `-a`, asserting sketch was running on a run that never mapped.
- `--noSingleFragProb` and `--skipQuant` help text, `docs/cli-flag-status.md` and the migration page corrected where they described pre-fix behaviour.

## One correction to Group 1

A FASTQ whose final record is **malformed rather than short** was told to "re-transfer the file". salmon cannot distinguish a truncated transfer from a corrupted one at that point, so it now describes what it observed and says as much. My own Group 1 test caught this when the wording changed.

## Tests

Seven new end-to-end tests covering each metadata field and each error path, including the controls that matter: `-l A` still agrees with the detector, genuine `--rad` still reports `rad_baked`, and the sketch warning still fires where sketch really runs.

Suite **338/0**, clippy clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a396dc2b3b25`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.