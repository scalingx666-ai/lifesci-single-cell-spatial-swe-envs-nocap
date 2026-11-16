# Issue

**Title:** Fix op.translate HCOP URL after EBI FTP drop

## Description

## Summary
- : HGNC has removed the entire `/pub/databases/genenames/` subtree from the EBI FTP mirror, so every `op.translate` call — and every `op.resource(..., organism=...)` call for a non-human organism — was failing with `HTTPError: 404`. The HCOP fifteen-column files are now fetched from HGNC's public Google Cloud Storage bucket (`https://storage.googleapis.com/public-download-files/hcop/...`), which is where HGNC currently publishes them (confirmed via bucket listing; `anole_lizard` object was last updated 2026-03-27). The move is only documented on https://www.genenames.org/help/hcop/ — there's no dedicated announcement on the HGNC news page, which is likely why this went unnoticed until the FTP directory was actually taken down.
- Drops a stray `pd.read_csv(url, ...)` at the end of `op.translate`'s download block that was silently re-downloading the HCOP file a second time immediately after `_download` + `_bytes_to_pandas` had already produced `map_df`, doubling the network cost per call and bypassing the retry logic in `_download`.
- Bumps version to `2.1.6` and adds a CHANGELOG entry.

## Test plan
- [x] `PYTHONPATH=src pytest tests/op/test_translate.py` — 7 passed (including `test_translate` parametrized over `mouse`, `anole_lizard`, and `fruitfly`, which hits the live bucket)
- [ ] CI green

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e1863048437`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.