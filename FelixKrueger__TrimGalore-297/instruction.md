# Issue

**Title:** chore(deps): forward dev → master to clear astro security alert

## Description

## Summary

Forwards `dev` into `master` so the public Dependabot security alert for `astro` clears.

Dependabot alerts are scoped to the **default branch** (master), so even though PR #296 fixed `astro ^6.1.9 → ^6.1.10` on `dev`, the repo's Security tab still shows **1 open alert** until master receives the fix.

## Why outside the usual release-time FF

Same justification as PR #292 (citation files): metadata/dep-only fix, no binary behavior change, doesn't affect anyone pinning to the v2.2.0 tag. Real pinning is tag-based, not branch-tip-based. Plus the visibility argument: a public security badge on the repo isn't a great look while the fix sits one branch away.

## Mechanics

Multiple commits since the last master push (citation FF):
- The merge-master-into-dev commit from earlier in this session
- PR #295 (dependabot config: target-branch: dev + npm ecosystem)
- PR #296 (astro 6.1.10)

A clean rebase will replay them linearly on top of master's current tip.

## Test plan

- [ ] After merge, the Dependabot alert for astro auto-dismisses (typically within minutes of Dependabot rescanning).
- [ ] No CI surface change — checks should mirror the green path PRs #294-#296 took.
- [ ] No effect on v2.2.0 tag, the v2.2.0 Zenodo deposit, or anyone consuming TrimGalore as a binary/crate.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `719de651073d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.