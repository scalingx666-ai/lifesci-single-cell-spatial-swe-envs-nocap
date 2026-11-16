# Issue

**Title:** chore(deps): route Dependabot to dev + add npm ecosystem for /docs

## Description

## Summary

Two changes to align Dependabot with the workflow model adopted in #285:

- **Add `target-branch: "dev"` to all ecosystems** so Dependabot opens PRs against `dev` (work trunk + docs auto-deploy source) instead of `master` (release pin). The mismatch was first surfaced by PR #294, which auto-opened against master and left the live docs site on the vulnerable `devalue@5.7.1` until master was manually merged into dev.
- **Add `npm` ecosystem for `/docs`** so the Astro/Starlight docs site dependencies get the same weekly + patch-minor-grouping treatment as `cargo` and `github-actions`. Without this, npm only got Dependabot attention via the security-advisory escape hatch (which is exactly how #294 opened despite zero npm config).

## Effect on future PRs

| Ecosystem | Before | After |
|---|---|---|
| cargo | weekly grouped PRs to master | weekly grouped PRs to **dev** |
| github-actions | weekly grouped PRs to master | weekly grouped PRs to **dev** |
| npm (/docs) | security-advisory-only, to master | weekly grouped PRs to **dev** + security advisories to **dev** |

## Test plan

- [ ] YAML validates (`python3 -c 'import yaml; yaml.safe_load(open(".github/dependabot.yml"))'`) — verified locally.
- [ ] Next Dependabot run (Monday) lands PRs on `dev`, not `master`.
- [ ] No effect on `cargo build`, tests, or CI matrix — config-only.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f27c54139378`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.