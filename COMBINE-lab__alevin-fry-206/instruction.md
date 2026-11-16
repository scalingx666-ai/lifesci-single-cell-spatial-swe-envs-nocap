# Issue

**Title:** chore: pre-release hygiene for the RAD v2 release (dead quant flag, spurious permit-list warning, compat docs, docs version)

## Description

## Summary

Small cleanups on `develop` before the RAD v2 release. None of them change counts or permit lists.

- `quant --multi-sample-output` has been parsed since 0.12, but nothing reads it. Its help text promised a default of "separate per-sample matrices", which never existed. quant always writes one combined matrix, and for multi-sample (e.g. Flex) input the rows are named `<sample>_<barcode>`.
- `generate-permit-list` warned `The provided permit list had barcodes of length 0, but the mapped reads have barcodes of length 16` in every mode except `-u`, including runs where no permit list was given.
- The Cargo.toml comment saying noodles must stay in lockstep with libradicl stopped being true when libradicl 0.21 landed (#198).
- The README and docs never said which RAD versions alevin-fry reads. alevin-fry 0.18.3 fails on piscem 0.24 (RAD v2) output with header-parse errors that say nothing about versions.
- `docs/source/conf.py` still said `0.18.2`, because `bump_and_publish.sh` never updated it.

## Changes

- **quant** (`src/main.rs`): `--multi-sample-output` still accepts `separate|combined|both`, so existing command lines parse. It is now hidden and has no default. When it is given, quant logs `--multi-sample-output=<v> is deprecated and has no effect; quant always writes one combined matrix, whose rows are named <sample>_<barcode> for multi-sample (e.g. Flex) input`.
- **generate-permit-list** (`src/cellfilter.rs`): the `cblen` vs permit-list length check now runs only for `UnfilteredExternalList` (`-u`), the only mode that loads a list whose length is known. The `-u` warning for a real mismatch and the warning for a missing `cblen` tag are unchanged.
- **Cargo.toml**: the comment now says noodles is used only by `convert`, and that libradicl >= 0.21 has no noodles dependency (`RadHeader::from_ref_names`), so noodles can be bumped on its own. Comment only.
- **Docs**: new *Compatibility* section in `README.md` and `docs/source/overview.rst`:
  - piscem >= 0.24 writes RAD v2, while salmon alevin and piscem <= 0.23 write RAD v1;
  - alevin-fry releases after 0.18.3 read both;
  - 0.18.3 and earlier fail with e.g. `invalid utf-8 sequence of 1 bytes from index ...` (scRNA) or `could not parse the RAD prelude` (ATAC);
  - `head -c 8 map.rad` prints `RAD_FILE` for a v2 file;
  - the same errors can also mean a truncated file.

  The note does not name the next release number. overview.rst now also lists piscem as a RAD producer.
- **Release tooling**: `conf.py` `release` is now `0.18.3`. `bump_and_publish.sh` now also does the following for `docs/source/conf.py`:
  - checks that the file exists;
  - rewrites its `release = '...'` line next to the crate version;
  - checks that the rewrite took;
  - reports it in `--dry-run`;
  - `git add`s it in the release commit.

## Behavior/compatibility

- No output changes. Matrices, featureDump.txt, quant.json and permit lists are content-identical to `develop`'s.
- `quant --help` no longer lists `--multi-sample-output`. Passing it still works, adds one WARN line, and does nothing else (as before). An invalid value is still a clap error.
- `generate-permit-list` no longer prints the bogus "length 0" warning in `-k`, `-f`, `-e` or `-b` modes. `-u` runs log exactly what they did before.
- No CHANGELOG edit: #202 adds the Unreleased section, and the release PR writes the notes.

## Testing

- `cargo fmt --check` passes (base is fmt-clean). `cargo clippy --all-targets` gives 0 warnings on both base and branch.
- `cargo test`: 108 passed, 0 failed, 3 ignored, on both base and branch. Merged with `test/rad-v2-integration`: 127 passed, 0 failed, 3 ignored; clippy has 0 warnings and fmt is clean.
- **generate-permit-list**, base vs branch release builds, on pbmc RAD v1 (piscem 0.23) and RAD v2 (piscem-main). Modes: `-k`, `-f 500`, `-e 1000`, `-b list`, `-u` 16-mer list, `-u` 12-mer list.
  - Permit outputs are identical. The bincode maps were compared as sorted pairs, because ahash makes the bytes differ from run to run.
  - generate_permit_list.json is identical apart from the paths.
  - After dropping timestamps, the logs differ by exactly one line: the removed bogus warning, in `-k`, `-f`, `-e` and `-b` modes only. `-u` with a 12-mer list still warns `length 12 ... 16` on both.
- **quant**, cr-like:
  - On a Flex RAD v2 collation (386 sample dirs, 9,452 `<sample>_<CB>` rows, 110,789 nnz), base without the flag matched each of: base with `separate`, branch without the flag, and branch with `separate`, `combined` and `both`. The matrix was compared joined by (row, col) name; featureDump.txt joined by key; quant.json minus cmdline/paths, with cell-number lists sorted. The same file set was written each time, and the WARN appeared only on branch runs that passed the flag.
  - On pbmc (1,141 cells), the results were the same.
- `--help` diff: only the `quant` help changes (3 lines removed). The help for generate-permit-list, collate, infer, convert, view, atac and the top level is identical.
- Sphinx 5.3 + furo builds the docs with 0 warnings on both base and branch. The rendered Compatibility section was checked, and the page title now reads "alevin-fry 0.18.3".
- `bump_and_publish.sh` was run in a sandbox clone whose `origin` is a local bare repo, with a pass-through `cargo-sanitize` stub.
  - `--dry-run` reports `release: 0.18.3 -> 0.18.4` and the `git add ... docs/source/conf.py` it would run.
  - A real run (without `--publish`) created the commit `chore(release): bump alevin-fry to v0.18.4`, touching Cargo.toml, Cargo.lock and docs/source/conf.py, and left a clean tree. The tag and push went to the sandbox only.
  - With the release line missing, the script stops early with `could not determine current docs release`.

## Merge notes

- **Suggested order** for this release: #203 (`fix/flex-sample-names`), #202 (`feat/200-umi-read-counts`), `fix/lenient-version-parsing`, this PR, `fix/errors-instead-of-panics`, and last #204 (`feat/probe-sum`) updated with `fix/204-explicit-flex-data-type`.
- **Heads checked on 2026-10-22:** develop edfd1aa, #202 8011bd5, #203 64c24d9, #204 d01f955, this branch 3ca52e4. None of them has moved since the previous check.
- **Clean merges.** This PR merges cleanly onto develop (`git merge --no-commit` and `git merge-tree`). It also merges cleanly with #202, #203, #204, each sibling branch and `test/rad-v2-integration` (1b3de59).
- **Full merge.** I ran the whole merge in the order above:
  - fmt is clean;
  - clippy has 0 warnings, with and without `--all-features`;
  - `cargo test`: 142 passed, 0 failed, 3 ignored.
  - Only the #204 step has conflicts, and they are between #202 and #204, not with this PR.
- **Nearby edits.**
  - #204 adds `--probe-mtx` directly above the `// Multi-sample output option` comment. This PR leaves that comment line alone, so the two changes don't touch.
  - The new warning is after the `--use-eds` check, away from the `dump_molecules` (#202) and `probe_mtx` (#204) lines.
- **Not in this PR:**
  - 1b3de59 on `test/rad-v2-integration` makes `--dump-molecules` work on Flex probe-level data. It belongs with whichever of #202 and #204 merges second (#204 in this order).
  - simpleaf's `feat/multiplex-quant-new-alevin-fry-options` passes `generate-permit-list --data-type flex`. It must ship with or after the alevin-fry release that contains #204 and `fix/204-explicit-flex-data-type`. The README/overview Compatibility note does not depend on it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01TtmwfkBMvwsCxdQrf4RTPN

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `edfd1aae5426`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.