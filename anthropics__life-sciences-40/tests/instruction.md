# Issue

**Title:** Add Consensus, Cortellis, and AdisInsight MCP servers

## Description

## Summary
- Adds three new remote MCP server plugins: **Consensus** (scientific literature search), **Cortellis** (Clarivate regulatory intelligence), and **AdisInsight** (Springer Nature drug pipeline intelligence)
- Registers each in `.claude-plugin/marketplace.json`
- Updates README with plugin IDs and authentication requirements

## Test plan
- [x] All `plugin.json` and `marketplace.json` validated as well-formed JSON
- [x] All three MCP endpoints reachable (return 401/403 as expected — auth required)
- [ ] Install via `/plugin install consensus@life-sciences` and confirm server connects after auth
- [ ] Repeat for `cortellis@life-sciences` and `adisinsight@life-sciences`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `20f100e7a28d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.