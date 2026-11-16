# Issue

**Title:** boot: cut cold-start costs in the sandbox entrypoint

## Description

## What

Three entrypoint changes that remove measured cold-start costs (staging, 2026-08-25, per-line container-log timestamps):

1. **Factory template cache: stop clearing it every boot.** A new-layout user's cold boot spent ~7 s `rm -rf`-ing the cache on the network volume + ~4.1 s re-materializing all 180 files — on every boot. `template_manager`'s smart-overwrite already handles image upgrades per file via `.factory_hashes.json` (update changed factory files, preserve user edits, skip the rest), so the unconditional clear is redundant. Kept as an escape hatch behind `PANTHEON_FORCE_FACTORY_REFRESH=true`.
2. **Background import prewarm.** Modal lazy-loads image layers: first `import pantheon.chatroom` measured 3–5.5 s vs 0.84 s warm. A detached `python -c 'import pantheon.chatroom'` at the top of the entrypoint pulls the files while the shell does its volume work.
3. **\[launch\] probes gated.** The sys.version/sys.prefix/ldd probes each spawn an interpreter (~1 s together on cold boot) — now behind `PANTHEON_BOOT_DIAG=true`; the free env echoes stay.

Plus an opt-in `PANTHEON_SETUP_HOOK_BACKGROUND=true` for the on-start hook (serial stays the default — 'hook finished before agent starts' is a guarantee user hooks may rely on).

## Verified

A/B test in a throwaway Modal sandbox on the staging image (`sha-4909aef`), original entrypoint vs this one, same env (`PANTHEON_DEFAULT_WORKSPACE=true`, `PANTHEON_FACTORY_TEMPLATE_MODE=global`):

| boot | entrypoint | result |
|---|---|---|
| 1st, empty volume | original | clear + full 180-file sync |
| 2nd | original | clear + full 180-file re-sync **again** (the every-boot cost) |
| 2nd | **this PR** | no clear, smart-overwrite syncs **0** files, bootstrap 0.028 s |
| 2nd, `FORCE_FACTORY_REFRESH=true` | **this PR** | clear + full re-sync (escape hatch works) |

Diag gating also verified (no interpreter-spawning probes by default).

Expected effect on staging cold boots: new-layout users ~-12 s, old-layout ~-4 s. Full investigation: measured boot anatomy artifact (admin 14.1 s vs google-user 39.6 s breakdown).

## Notes

- Based on `feat/desktop-resolution` (what staging runs) to avoid conflicts with the in-flight display-streaming work; only `docker/docker-entrypoint-dual-mode.sh` is touched.
- Not deployed anywhere yet.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01MjLiwbbQ9h4iSKDpwUy9Jg

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e83363f4b4cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.