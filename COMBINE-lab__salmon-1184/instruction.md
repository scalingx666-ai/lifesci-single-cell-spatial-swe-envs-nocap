# Issue

**Title:** fix(website): bump nanoid to 3.3.18 (GHSA-2v37-7h3g-55p8)

## Description

Clears **Dependabot alert #16** (high-severity chip; actual CVSS **5.9 medium**, availability-only).

## What it is

`nanoid` < 3.3.18 can loop indefinitely when a custom generator is called with `size` 0 — a DoS. It is a **transitive** dependency of the **docs website** only: `astro → vite → postcss → nanoid`. It is **not part of the salmon binary**, and postcss always calls nanoid with a fixed positive size, so the vulnerable path is not reachable here. Cleared anyway to take the high-severity alert off the default branch before the 2.6.0 tag.

## The change

`3.3.18` satisfies postcss's existing `^3.3.16` requirement, so this is a single in-range patch bump. The diff is exactly nanoid's three fields:

```
-      "version": "3.3.16",
-      "resolved": ".../nanoid-3.3.16.tgz",
-      "integrity": "sha512-bzlKTyNJ7+...",
+      "version": "3.3.18",
+      "resolved": ".../nanoid-3.3.18.tgz",
+      "integrity": "sha512-DTg4MJbGMW...",
```

Edited directly rather than via `npm update`, because `npm update` under the local npm 8 also strips `libc` optional-dependency metadata that a newer npm wrote (106 unrelated deletions) — churn I did not want in the lockfile. The `3.3.18` version/URL/integrity are npm's own resolved values against the registry. JSON validated; postcss still resolves nanoid via its unchanged `^3.3.16` range.

No code, no salmon impact — a docs-site lockfile hygiene fix.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `026a85d99947`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.