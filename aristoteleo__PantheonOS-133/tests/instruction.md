# Issue

**Title:** feat(skills): Pantheon Store skill discovery, adoption & usage feedback

## Description

Gives the agent **store-awareness**: before a task it can search the marketplace for the most relevant skill, decide whether to adopt it from the quality signal, use it ephemerally, and — once done — feed back whether it actually worked. Closes the quality loop between the static AI review and real usage.

Reuses the existing `SkillToolSet` (`pantheon/internal/learning_system/`) — no new toolset. Local skills always take precedence; the store is the fallback when nothing local fits.

### Scope 1 — discovery + adoption (read path)
- **`skill_search_store(query, limit=8)`** → GET hub `/api/store/recommend`. Lexical (FTS) ranking over name/display/description/category + the reviewer's `best_for`, joined with the `pantheon-reviewer` AI evaluation. Returns ranked candidates with `verdict` / `overall` / `rating` / `best_for` / `not_for` / `caveats`, excluding skills already installed locally and any `not_recommended`. The agent decides from this payload.
- **`skill_adopt(name)`** → GET `/api/store/packages/{name}/download`. Loads content **ephemerally** into the task context (not installed to `~/.pantheon`); followed like a local skill for this task only.

### Scope 2 — post-task usage feedback (write path)
- **`skill_rate(name, rating, comment)`** → POST `/api/store/packages/{name}/reviews` as the **user's real review**. Token resolves from `PANTHEON_STORE_TOKEN` (runtime-carried session token) or the `pantheon store login` file; no-ops with a clear hint if neither is present, so it never fails the task. This makes the store's quality signal **usage-validated**, layered on top of the static rubric.

`SKILLS_GUIDANCE` (prompts.py) is extended with a marketplace section (when to search/adopt, how to choose) and a nudge to rate adopted skills after the task.

### Validated e2e (against staging)
- **Scope 1:** agent searched "molecular docking", correctly **rejected** the highest-rated candidate (a SPR/BLI-kinetics skill whose `best_for` didn't match docking) and adopted `diffdock` instead — proves the decision payload drives real choices.
- **Scope 2:** agent adopted `openclaw-medical_diffdock`, summarized it, then `skill_rate(rating=4, comment=…)` — the review **landed on staging** attributed to the real user, ★4 alongside `pantheon-reviewer`'s static ★3 (avg 3.5/2). Closed loop confirmed live.

Hub `/recommend` endpoint is already merged (#24) and deployed to staging. Lexical retrieval is v1; semantic-embedding ranking is a deferred v2.

**Draft — not for merge to main yet.**

---

### Auth model (who can give feedback)
Read ops (search/adopt) are **anonymous**; only feedback (`skill_rate`) is posted as the user, so only it requires login — same split as the existing `install_store_package` (anonymous download, login-gated record).

`_store_credentials()` is the single source of truth for the user's store identity:
| Mode | "logged in" = | token source |
|---|---|---|
| Local CLI | ran `pantheon store login` | `~/.pantheon/store_auth.json` |
| Hosted | platform session | `PANTHEON_STORE_TOKEN` (+ `PANTHEON_STORE_USER`) injected at agent launch |

No password handling in the agent loop. Unauthenticated `skill_rate` returns `needs_login` (no network) and the agent is told to prompt the user to log in rather than silently skip; 401/403 (expired) is distinguished from 404 (not found); the success hint is attributed to the username.

### Follow-ups (NOT in this PR)
- **Hub/server side:** when the hosted platform launches an agent session for a logged-in user, mint/forward that user's store JWT into the agent env as `PANTHEON_STORE_TOKEN`. This is the only missing piece for hosted feedback; the agent side already consumes it.
- **`/recommend` v2:** semantic-embedding ranking (current v1 is lexical FTS).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee55298da535`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.