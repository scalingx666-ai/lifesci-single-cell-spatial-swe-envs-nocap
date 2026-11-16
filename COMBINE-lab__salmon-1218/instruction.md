# Issue

**Title:** fix(website): drop legacy markdown.remarkPlugins so the Astro docs build works

## Description

## Problem

The documentation website (`website/`, an Astro + Starlight project) has failed to build/deploy since ~2026-08-30. Building it reproduces the failure:

```
`markdown.remarkPlugins`, `markdown.rehypePlugins`, and `markdown.remarkRehype`
run on the `unified` processor from `@astrojs/markdown-remark`, which is no
longer installed by default now that Sätteri is the default Markdown processor.
Install it with:
  npm install @astrojs/markdown-remark
```

**Root cause:** Astro 7.x made **Sätteri** the default Markdown processor and stopped pulling in `@astrojs/markdown-remark` transitively. The site's `website/astro.config.mjs` still used the legacy `markdown.remarkPlugins: [remarkGfm]` API, which requires that package and the old `unified` processor — so Astro's config validation now throws before the build starts.

## Fix (minimal, no Astro bump)

GitHub-Flavored Markdown (tables, strikethrough, autolinks) is now **on by default** in the Sätteri processor (`markdownConfigDefaults.gfm === true`), and `@astrojs/mdx` inherits that setting — so GFM already applies to both `.md` **and** `.mdx` pages without any extra config. The explicit `remarkPlugins: [remarkGfm]` block is therefore redundant.

- **`website/astro.config.mjs`** — remove the legacy `markdown: { remarkPlugins: [remarkGfm] }` block and the `remark-gfm` import; replace the comment to document that Sätteri handles GFM.
- **`website/package.json`** — drop the now-unused direct `remark-gfm` dependency (it remains available as a transitive dep of `@astrojs/mdx`, which applies GFM internally).
- **`website/package-lock.json`** — regenerated to match.

Rather than re-adding `@astrojs/markdown-remark` and keeping the deprecated API (which Astro warns "Will be removed in a future major" and which would switch the whole pipeline back to the legacy `unified` processor), this migrates to the supported approach. **Astro is intentionally left at its current pin** (`^7.2.9` on develop) — the Astro upgrade is handled separately by dependabot PRs #1209 / #1203.

## Verification

Before: `npm ci && npm run build` → **config validation error** (shown above), exit 1.

After (Node 22, develop's `astro@7.2.9`): `npm ci && npm run build` → **exit 0**, 13 pages built, `dist/index.html` present, and GFM tables still render as `<table>` in the `.mdx`/`.md` pages (e.g. `guides/library-types`: 5 tables, `reference/cli`: 9, `migrating/from-cpp`: 2, `reference/output-formats`: 6). Output is equivalent — GFM still enabled.

## ⚠️ Where the deploy actually runs

`.github/workflows/docs.yml` triggers the GitHub Pages deploy on push to **`main`/`master`** — **not** `develop`. This PR targets `develop` per the repo's contribution convention, but **the deploy is currently broken on `master`**. For the website deploy to go green, this fix must reach `master` — via the next `develop → master` merge, or a direct cherry-pick of this commit onto `master`. (The identical broken config is present on `master` today.)

Do not merge without the maintainer's review.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Xg1hUw9i95rJikA6eL2WNH

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34f99a1aa6cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.