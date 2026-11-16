# Issue

**Title:** chore(branch): rename optimus_prime → dev post-v2.1.0 GA

## Description

## Summary

Post-v2.1.0 GA branch-layout cleanup. PR #214 collapsed the two-trunk model on 2026-05-04 (Rust v2 → master, Perl 0.6.11 → preserved at the `0.6.11` git tag), so the `optimus_prime` name no longer carries meaning. Renamed the branch on GitHub and swept all 17 in-tree references.

- 8 files, 19 / 19 insertion-deletion pairs
- 3 workflow files (CI/docs push+PR triggers, release.yml branch gate + error message)
- README + docs/install.md (CI badge → master, `cargo install --branch dev` snippet, Docker `:dev`-tag explanation reworded)
- benchmarks.md + perf_data README (3 `tree/optimus_prime/...` URLs repointed at `master` since the perf data is archived/immutable)
- CLAUDE.md (opening paragraph reframed for post-GA reality)

Two `optimus_prime` mentions are deliberately retained as historical context (one CI comment, the CLAUDE.md paragraph itself).

GitHub auto-redirects pre-rename URLs and git fetch-by-name for ~6 months. The only user-facing behaviour change is the `cargo install --branch dev` line in the README/install docs.

## Test plan

- [ ] CI (Lint, Rust Tests ubuntu+macos, Coverage, Reproducibility, Security audit, Validate vs Perl) green on the rename branch
- [ ] Pages deploy: docs site rebuilds from `master` after merge with the updated benchmark URLs
- [ ] Smoke: `cargo install --git https://github.com/FelixKrueger/TrimGalore --branch dev trim-galore --force` resolves

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3f6be57a7da5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.