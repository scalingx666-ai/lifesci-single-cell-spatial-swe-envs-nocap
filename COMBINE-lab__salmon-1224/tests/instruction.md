# Issue

**Title:** chore: sync master (v2.8.0 release) back into develop

## Description

**⚠️ Please merge this with "Create a merge commit", not squash.** Recording master as merged into develop is the point of this PR. #1220, #1222 and #1223 were each squash-merged, so git never recorded the two branches as merged, and every develop ↔ master merge since has conflicted.

This brings the v2.8.0 release back into `develop`:
- the workspace version bump to **2.8.0** (`ed926b8f`, from `bump_and_publish.sh`);
- `docs/release-notes-2.8.0.md`, which was committed on the release branch only.

`develop` had no commits since the release, so the merged tree is **byte-identical to `master`'s**. The only conflicts were the version lines in `Cargo.toml`/`Cargo.lock`, resolved to master's 2.8.0. It builds with `--locked`.

With a merge commit, the next release merge (develop → master) is conflict-free.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Xg1hUw9i95rJikA6eL2WNH

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf7c8ef0af3e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.