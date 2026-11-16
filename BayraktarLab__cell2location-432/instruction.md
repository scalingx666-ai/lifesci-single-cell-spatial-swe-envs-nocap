# Issue

**Title:** Add @claude GitHub integration

## Description

## Summary
- Add GitHub Actions workflow (`.github/workflows/claude.yml`) that triggers when `@claude` is mentioned in issues or PR comments, enabling automated issue fixing and code review
- Add `CLAUDE.md` with project guidelines (code style, architecture, testing conventions) so Claude understands the codebase
- Add local test notebooks and artifacts to `.gitignore`

## Setup required after merge
1. Install the [Claude GitHub App](https://github.com/apps/claude) for this repository
2. Add `ANTHROPIC_API_KEY` as a repository secret (Settings > Secrets > Actions)

## Test plan
- [ ] Merge PR and install the Claude GitHub App
- [ ] Add `ANTHROPIC_API_KEY` secret to the repository
- [ ] Test by commenting `@claude` on an issue or PR

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c01046d34216`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.