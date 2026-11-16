# Issue

**Title:** feat: integrate OpenMHS Model Hardware Standard through MCP

## Description

OpenAI4S can discover and control OpenMHS devices through ordinary MCP connectors. [OpenMHS](https://github.com/PKU-YuanGroup/OpenMHS) is the open-source Model Hardware Standard; its project domain is `mhs.openai4s.org`. The SDK and reference host remain optional, and endpoint connectors are enabled through operator configuration.

The host route journals command intent, records receipts and verified evidence, and reconciles unknown outcomes before retrying. Tool discovery must succeed before the adapter can route an ordinary call, so a discovery failure cannot fall through to an unjournaled command. A device-bound emergency stop bypasses the ordinary approval prompt while retaining persisted MCP deny rules, connector authorization, endpoint/device binding and auditing. Both stop entry points use the canonical connector permission identity, including inherited conversation and project rules. Resets, permits and hardware access retain their operator controls.

Missing optional packages leave the core available. If an installed integration or one of its dependencies is broken, its import error is now reported instead of silently disabling the integration. The English and Chinese guides describe installation and endpoint setup.

Validation at `7c060658`:

- Full offline suite: 12,480 passed, 43 skipped.
- Targeted host/MCP/permission tests: 138 passed, including regressions reproduced before the fixes. Explicit kernel, agent and gateway checks: 290 passed.
- Real OpenMHS stock-host route against local simulated endpoints: 10 tests passed.
- Full pre-commit, mypy (25 files), bilingual directory documentation, source credential scan and `git diff --check`: passed.
- Offline PR scenario contracts: 38 passed. Chromium workbench smoke against an isolated daemon: passed.
- Updated with current `main`; GitHub CI runs on the current PR head.

No hardware run is claimed. OpenMHS keeps its device limits, interlocks, access control and emergency stops. Pages deployment is deferred at the owner's request.

The original integration was prepared with Codex (gpt-6.1-sol) and reviewed by Claude; the follow-up cleanup was prepared with Codex.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `91bc208aefa7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.