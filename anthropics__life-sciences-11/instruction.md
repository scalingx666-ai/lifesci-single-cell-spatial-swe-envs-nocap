# Issue

**Title:** Remove Benchling plugin from marketplace

## Description

## Summary
- Remove Benchling plugin entirely from the marketplace
- Benchling uses tenant-specific URLs which are not supported by the plugin system
- Added note in README documenting the removal

## Changes
- Removed benchling-mcp entry from marketplace.json
- Removed all Benchling references from README.md
- Deleted benchling/.claude-plugin/plugin.json
- Added "Removed Plugins" section to README explaining why

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b21291776c62`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.