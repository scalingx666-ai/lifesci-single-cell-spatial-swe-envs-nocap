# Issue

**Title:** feat(browser): popups become tabs, and pages carry a favicon

## Description

/#185, the login-and-polish pass on the shared browser.

**Popups become tabs.** A `window.open()` — every "Continue with Google" / "Sign in with GitHub" OAuth flow — used to fold back into the opener and lose the login. Now the popup is adopted as its own attached, streamable page and announced to the UI via the opener's `X-Popup` frame header (drained once, idempotent). The Atrium Browser opens and focuses it as a tab; the login finishes there and the opener — the SAME shared Chromium — sees the result.

**Favicons.** Each page reports its `<link rel=icon>` href (or `/favicon.ico`) via `X-Favicon`, so tabs show real site icons (chip fallback on the frontend).

Both headers join `Access-Control-Expose-Headers`.

Verified off-sandbox against real Chromium: `window.open` adopted as a pollable page streaming its own frames + announced exactly once; real favicons resolved for github/wikipedia. Frontend (tabs, New Tab home, omnibox search, popup→tab, favicon) is in pantheon-atrium.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9154534c9a3d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.