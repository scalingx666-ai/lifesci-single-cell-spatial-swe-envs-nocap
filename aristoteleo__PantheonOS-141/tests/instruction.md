# Issue

**Title:** chore(factory): retire the legacy {{skills}} prompt

## Description

Retires the prompt-based `{{skills}}` mechanism, now superseded by the always-on learning system.

### Why
`{{skills}}` expanded to `prompts/skills.md` (static "scan the skills dir with shell commands" guidance). The learning system (`LearningPlugin`, always registered) already injects `SkillToolSet` **and** a runtime skill index into every agent — so the placeholder was redundant, and when present it layered a second, conflicting guidance block (shell-scan vs `skill_view` tool) onto the prompt. `prompts/skills.md` had also been untouched since Dec 2025, while the learning system shipped Apr 2026.

### Changes
- Delete factory `pantheon/factory/templates/prompts/skills.md`.
- Update the `PromptResolver` docstring example (it referenced the deleted prompt) to a generic name.
- Remove the now-obsolete `test_builtin_skills_prompt_has_params` test.

### Safety
- No factory agent or team references `{{skills}}` (verified) — only the docstring did, which is updated. So nothing is left with an unresolved placeholder.
- The learning system / `SkillToolSet` and the `skills/` template directory are untouched.
- Pairs with the front-end PR that removes the corresponding Features-panel toggle (Nanguage/pantheon-ui#18).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6df814bb8843`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.