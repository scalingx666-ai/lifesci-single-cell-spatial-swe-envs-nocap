# Issue

**Title:** chore(deps): robust high-compression test + group Dependabot patch/minor

## Description

## Summary

Two small housekeeping changes after the v2.1.0 GA Dependabot wave:

1. **\`src/parallel.rs\` — bump high-compression test input from 200 → 5,000 reads.** The 200-read fixture (~13 KiB) was small enough that level-6 gzip framing overhead occasionally erased the 2-3 byte compression win over level-1. flate2 1.1.5 → 1.1.9 (Dependabot #274) tipped it the wrong way: 571 → 573 vs 573 → 571, failing the \`size_high < size_default\` assertion. 5,000 reads (~325 KiB) gives level-6 enough material to amortise the constant overhead so the assertion is robust against future patch-level flate2 tweaks. Test still runs in <50 ms — confirmed locally.

2. **\`.github/dependabot.yml\` — add \`groups\` blocks for cargo + github-actions.** Patch + minor bumps now batch into a single weekly PR per ecosystem. Major bumps continue to open individually so breaking-change reviews stay focused. Collapses the typical post-merge inbox surge (3 PRs × ~3 events ≈ 9 emails) to 1-2 emails per Monday.

After this lands, Dependabot will rebase #274 against master; the test fix should let it go green and merge cleanly.

## Test plan

- [ ] \`Lint (fmt + clippy)\` green
- [ ] \`Rust Tests (ubuntu-latest)\` and \`Rust Tests (macos-latest)\` green
- [ ] \`Coverage\`, \`Reproducibility\`, \`Security audit\`, \`Validate vs Perl\` green
- [ ] After merge: re-run #274 CI; confirm flate2 bump now passes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `466dd128fbe2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.