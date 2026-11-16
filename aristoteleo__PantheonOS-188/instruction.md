# Issue

**Title:** feat(browser): scroll metrics + scroll input for the UI scrollbar

## Description

Headless Chromium renders no native scrollbar (confirmed: neither the CDP screencast nor Playwright's own screenshot shows one, and `::-webkit-scrollbar` CSS doesn't paint offscreen). So the Atrium Browser draws its own scrollbar overlay — this PR gives it the data and the control:

- **`status_headers`** adds `X-Scroll = "scrollY,scrollHeight,innerHeight"` (a cheap eval, only on repaints), listed in `Access-Control-Expose-Headers`.
- **`dispatch`** accepts `{t:"scroll", y}` → `window.scrollTo(0, y)` for thumb drags.

Frontend overlay (thumb sized/positioned from X-Scroll, draggable) is in pantheon-atrium (already merged). Forward-compatible: an older image without X-Scroll just shows no scrollbar; the page still scrolls by wheel.

Verified off-sandbox: `X-Scroll 0,9581,800` → `scroll(1500)` → `1500,9581,800`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8dbcaf9d6ba5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.