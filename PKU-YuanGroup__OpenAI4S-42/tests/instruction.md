# Issue

**Title:** fix(webui): route web sharing through the versioned API prefix

## Description

## What is broken

Web sharing is non-functional on `main` right now. Its six frontend fetches address the un-versioned surface directly:

| `openai4s/server/webui/app.js` | call |
| --- | --- |
| 4240 | `fetch("/api/share/status")` |
| 4241 | `fetch(\`/api/frames/${fid}/shares\`)` |
| 4271 | `shareCall("PUT", "/api/share/settings")` |
| 4309 | `shareCall("PUT", \`/api/shares/${id}\`)` |
| 4314 | `shareCall("DELETE", \`/api/shares/${id}\`)` |
| 4342 | `shareCall("POST", \`/api/frames/${fid}/shares\`)` |

`#41` moved the contract to `/api/v1` and removed the un-versioned surface with no legacy alias (a deliberate, owner-frozen decision — the only clients are first-party). So every one of these 404s, and every sharing control in the UI fails.

Verified against a live daemon:

```
/api/v1/share/status  -> 200  {"state": "disabled", "configured": false}
/api/share/status     -> 404
```

## Why nothing caught it

Both changes were correct in isolation and landed from separate branches (#38 and #41). The share routes have server-side tests, and these six literals only execute in a browser, so the full offline suite stayed green through the merge.

## The fix

Route all six through the existing `API` constant (`app.js:83`, `"/api/v1"`), which every other request in the file already uses.

Plus a static contract test that rejects any `/api/...` literal outside that constant, so the next route added off-prefix fails offline instead of in a user's browser. That test fails on `main` today and passes here.

## Verification

- `tests/test_webui_static_contract.py` — 33 passed
- Full offline suite — 2107 passed, 3 skipped
- Live daemon — the versioned route serves, the un-versioned one 404s (above)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f7bb29f1ea15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.