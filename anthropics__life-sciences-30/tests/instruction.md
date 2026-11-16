# Issue

**Title:** Add scientific-problem-selection skill to marketplace

## Description

## Summary
- Adds the missing scientific-problem-selection skill to the marketplace.json configuration
- Updates README.md with installation instructions and documentation
- Fixes issue #29 where the skill existed but was not discoverable in the marketplace

## Changes
- Added entry in `.claude-plugin/marketplace.json` for scientific-problem-selection
- Updated README.md Quick Start section with installation command
- Added detailed documentation in Skills section with use cases

## Testing
After merging, users should be able to install the skill with:
```
/plugin install scientific-problem-selection@life-sciences
```

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4cb96c4f11c5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.