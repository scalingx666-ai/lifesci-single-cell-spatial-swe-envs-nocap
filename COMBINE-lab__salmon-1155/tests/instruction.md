# Issue

**Title:** audit: inert flags say so, provenance tells the truth (B8/B9, F18–F20)

## Description

Five findings from the #1140 pre-2.6.0 behavior audit, plus one adjacent parity fix. All warn-or-truth changes; no quantification math touched.

- **B8** — `-i/--index` alongside `-a` or `--rad` was accepted and silently never consulted. Both branches now warn.
- **B9** — `-t/--targets` was a silent no-op in **both** reads paths: one-pass never wired it, and the deterministic driver wired it into a fallback that was unreachable (with bias on, the index's own sequences always win; with bias off, nothing reads them). Reads mode now warns and ignores it, the dead wiring and the false "honoured as a fallback" comment are gone, and the `-t` help text no longer claims it "enables the error model" (only true under `--online -a`; the default alignment path takes `--errorModel`).
- **F18** — the deterministic `-a` and genome-projection writers baked the user's explicit `-l` as the RAD library-format tag (expected-wins), the reverse of the reads-mode writer — so `library_type_mismatch` could never fire on those paths and `detected_library_type` echoed the user's assertion back as an observation. The tag now bakes detected-wins; in-pass strand filtering keeps expected-wins, as everywhere else.
- **F19** — the truncated-mass warning existed only in the deprecated drivers while every `quantify_rad` path computed and recorded the value silently. Hoisted into the shared output writer: all five drivers now warn exactly once, next to where the value is written.
- **F20** — `extra_diagnostics` was documented as appended on every path but only `quantify_rad` honoured it; the online `-a` path dropped driver-supplied diagnostics. The append moved to the shared meta writer (`quantify_rad` still *speaks* them in its log; recording happens once).
- **Adjacent** — `write_alignment_rad`'s bias gate now includes `!no_length_correction` like its reads-mode twin, so `-a --noLengthCorrection --gcBias` no longer spends a naive eq-class pass + seed EM baking `initial_abundances` the requant is guaranteed to ignore.

Tests: a wrong explicit `-l` over ISF alignments now fires `library_type_mismatch` and the diagnostic names the observed format (fails on develop), with a matching-`-l` control; driver diagnostics reach `meta_info.json` on the online alignment path (fails on develop).

Full workspace suite 317/0; clippy clean (the two pre-existing `chunks_exact` warnings in untouched files are queued for the batch G cleanup PR).

Remaining audit ledger after this: batch E (warn-and-ignore matrix, next up), batch G (docs + dead code), and C/D pending @BenjaminDEMAILLE.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2c5beaa56a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.