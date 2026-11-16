# Issue

**Title:** Restore the output contract on every RAD-based path (pre-2.6.0 audit, batch A)

## Description

The release-blocking batch from the #1140 behavior audit — the six output-contract defects on the deterministic default plus the `-a`/reads mode-dispatch hole, all hand-verified before fixing. This gates #1150 (the flip): the default path cannot ship emitting decoy rows.

- **Decoy exclusion, end to end.** Phase 1 bakes the decoy boundary into the RAD header (`first_decoy_index`/`num_decoys` tags on `IndexProvenance`); the requant writer excludes the block from `quant.sf`, bootstrap `names.tsv.gz`/`bootstraps.gz`, `ambig_info.tsv`, and `num_valid_targets`, via `quant_row_indices` hoisted to `salmon-core` and shared with reads mode. Boundary-less RADs (piscem, BAM-derived, older salmon) are unchanged. E2E test drives the real binary: decoy-aware index → `--deterministic` → same decoy-free row set as one-pass.
- **`cmd_info.json` preserved** (phase 2 keeps phase 1's true invocation record) and **`lib_format_counts.json` names the read files** instead of `[]`.
- **`meta_info.json` placeholders fixed**: `samp_type` derived (`bootstrap`/`gibbs`/`none` — tximport keys off it), `serialized_eq_classes` from the dump flags, `num_decoy_fragments` from the baked counter.
- **Genome projection bakes `MapCounters`** — real `num_processed` in its requant's metadata.
- **Single-end `frag_length_source` reports `"prior"`** — the FLD never observed a fragment length.
- **`-a` conflicts with `-1/-2/-r`** at the parser instead of silently quantifying the BAM and dropping the FASTQs.

Tests at three levels: parser (clap conflict), RAD (decoy/meta contract with baked provenance + counters, plus the boundary-less compatibility case), and full-binary e2e (decoy round trip, cmd_info/read_files preservation, SE provenance). Workspace suite **312 passed / 0 failed**; clippy/fmt clean.

Sequencing: merges before #1150; the flip rebases on top (trivial — different regions except `AlignQuantOptions`, both-additive).

.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9e2bdbe401eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.