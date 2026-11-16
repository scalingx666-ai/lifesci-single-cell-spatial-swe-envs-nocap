# Issue

**Title:** chore: sync master (v2.7.0 release) back into develop

## Description

Brings `develop` up to date with the commits that were made directly on `master`:
- the v2.7.0 workspace version bump and the release merge commit;
- five dependabot website bumps: #1208 (svgo), #1210 (smol-toml), #1211 (sharp), #1212 (js-yaml), #1215 (devalue).

**Why now:** without this sync, the develop → master merge for 2.8.0 conflicts in `website/package.json` and `website/package-lock.json`. It also means #1198, which was branched from `master`, can be retargeted to `develop` without pulling these commits in.

**Conflict resolution** in `website/package.json` keeps both sides:
- from `develop`: starlight 0.41.9, astro 7.2.9, and the removal of the direct `remark-gfm` dependency (#1218);
- from `master`: sharp 0.35.4.

The lockfile is regenerated from develop's with npm (Node 22), with master's transitive bumps applied (svgo 4.1.0, smol-toml 1.9.0, js-yaml 4.3.2, devalue 5.9.4).

**Verification:**
- `astro build` succeeds (13 pages).
- `cargo build --locked` succeeds.
- The workspace tests pass.

**Merge note:** please merge with a **merge commit**, not a squash, so git records `master` as merged into `develop`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Xg1hUw9i95rJikA6eL2WNH

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e54211e241a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.