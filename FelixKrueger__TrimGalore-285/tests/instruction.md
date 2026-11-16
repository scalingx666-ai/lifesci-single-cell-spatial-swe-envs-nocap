# Issue

**Title:** ci(docs): revert deploy-gate; dev is the canonical live-content source

## Description

## Summary

Reverts the deploy gate from #284. The gate was based on a "master = stable, dev = WIP" model that doesn't fit the actual workflow: in practice **dev is where all content lands first**, and master is just the release pin updated by FF from dev right before a release cut.

Under the gate, a docs improvement on dev wouldn't show up on www.trimgalore.com until a release — that's wrong. Docs should track dev's HEAD and reach users immediately.

## Behaviour after this lands

| Trigger | Build | Deploy |
|---|---|---|
| push to \`master\` (release-time, rare) | ✅ | ✅ — defensive redeploy |
| push to \`dev\` (the canonical content channel) | ✅ | ✅ — site updates immediately |
| \`workflow_dispatch\` (any branch) | ✅ | ✅ |

So dev pushes update the live site immediately. Master pushes (rare, only at release time) trigger a redeploy of the same content as a no-op safety net.

## Why a quick revert rather than just editing further

PR #284 was merged ~30 minutes before this; the gate hadn't yet fired in the wild (no docs-touching push to dev since #284 landed). Cleanest history is "added gate → reverted gate" rather than mutating the gate's intent in place — the diff is honest about the decision flip.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dbad74ad9376`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.