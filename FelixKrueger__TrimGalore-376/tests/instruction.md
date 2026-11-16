# Issue

**Title:** fix(docs): stop KaTeX eating prose, repair the pigz benchmark image

## Description

Two rendering defects that are **live on www.trimgalore.com right now**, plus a guard in both docs workflows so neither class recurs. No change to the tool — this is entirely the documentation site.

Both were found while reviewing the plan for `changelog-mirror-automation`, which makes the changelog page an unattended build artefact of `CHANGELOG.md`. That raises the cost of a silent render bug, so these are fixed first.

## `$` in prose was being parsed as maths

`astro.config.mjs` wires `remarkMath`, which by default treats a single `$` as an inline-maths delimiter. Prices in prose were consumed:

| | rendered |
|---|---|
| source | `~$7 vs ~$41 per 1000-sample cohort at AWS $0.05/vCPU-hour` |
| **live site** | `— ~7vs 7 vs ~7vs 41 per 1000-sample cohort at AWS $0.05/vCPU-hour` |

Two `$` deleted, one `~` deleted, `7vs` italicised as maths variables, content duplicated by KaTeX's MathML+HTML double emission.

`performance/benchmarks.md` is worse — **two** nodes, the second a parse *failure* rendered as a red `katex-error` span containing a whole sentence, with a literal `\~` leaking through, orphaned `**` and a mis-scoped `<strong>`.

Fixed with `singleDollarTextMath: false`. `$$` display maths is *structurally* unaffected, not merely observed to survive: `micromark-extension-math` passes options only to `mathText`, never to `mathFlow`. Swept all 30 content entries plus `CHANGELOG.md` — **nothing anywhere relies on single-dollar inline maths**, so the fix has no legitimate casualty. `performance/clumpy.md` keeps its one node.

Not fixed at the config layer for the mirror-image hazard (`~`): Astro exposes `markdown.gfm` as a **deprecated boolean only**, so reaching `remark-gfm`'s `singleTilde` would mean `gfm: false` plus re-adding the plugin by hand — risking tables, which that very page uses, to defend one line.

## The tilde escapes on `benchmarks.md` are load-bearing

Worth flagging because they look like leftovers from the `$` problem and an earlier draft of this change removed them. **They defend against GFM single-tilde strikethrough**, a separate mechanism unaffected by the `remarkMath` change.

Measured — config fix applied, escapes removed:

```
<del> site-wide          1     <-- struck-through prose ships
katex-error site-wide    0
class="katex" benchmarks 0
```

Every maths-based check passes while the page renders the sentence inside `<del>` with a `**` bold pair collapsed to literal asterisks. A one-line source comment now marks them.

Whether `~` opens strikethrough depends on attention flanking, which is why the changelog line is safe and this one is not: in `**~$41` the `~` is preceded by `*` so it is a valid right-flanking closer; in `— ~$7 vs ~$41` the second `~` is space-preceded and cannot close.

## An image path that existed nowhere

The v0.6.0 `-j/--cores` entry carried `<img src="docs/Images/pigz_bench.png">`. That directory has never existed in the repository, so the image was broken in **both** the GitHub and web renderings, and the asset was orphaned — referenced only by the two broken tags and absent from the build's optimised images.

Moved to `docs/public/images/` and referenced by site-absolute URL. Self-hosting rather than `raw.githubusercontent` removes branch pinning as a concept — the two in-repo precedents both pin `master` while the site deploys from `dev` — and one absolute tag serves both renderers, which a relative path cannot: GitHub resolves relative to the file, Astro relative to the page URL. `alt` added.

## Why `katex-error` alone was not a guard

`rehype-katex` emits `katex-error` **only when KaTeX fails**. A *successful* accidental parse emits `class="katex"` and no error span — and that is exactly the changelog defect above, which renders 3 `class="katex"` and **0** `katex-error`.

A first version of this step asserted `katex-error`, `src="docs/` and `<del>`. Extracted from the parsed YAML and run under `bash -e` against four real directories:

| tree | first version | shipped version |
|---|---|---|
| fixed build | 0 | 0 |
| pre-fix build | 1 | 1 |
| **changelog corruption only** | **0** | **1** |
| **no `dist/` at all** | **0** | **1** |

It passed on the real pre-fix build only because the unrelated image bug happened to sit on the same page. Reword `benchmarks.md` so KaTeX parses cleanly, revert the config, and you get corrupted prices with a green build.

So the step also allowlists `class="katex"` to `performance/clumpy` — the only legitimate maths on the site. That allowlist is a maintenance point: a second maths page must be added to it. It is the right trade against a sentinel that cannot see the defect.

Real directories, not symlinks: **BSD `grep -r` does not descend into a symlinked `dist`** and returns 0 on a tree that plainly contains the pattern. That produced a false pass during verification before being caught.

Three further properties, each from a measured failure:

- **`test -d dist` first.** `grep` exits 2 on a missing directory and `if` swallows it, so the step passed with no output to check. Masked in `ci.yml` by the preceding step; live in `docs.yml`.
- **The image pattern is anchored** to `<img[^>]*src="[Dd]ocs/`, not the bare string. Double quotes survive unescaped inside `<code>`, so prose *documenting* this bug would otherwise fail the build — the CHANGELOG entry in this PR avoids that only by phrasing. `[Dd]` covers this filesystem's case-insensitivity.
- **A `fail` accumulator, not fail-fast**, so co-occurring defects surface in one run. The whole step takes 0.09 s over 238 files.

`<del>` never shipped to the live site; it is prophylactic. The ban is site-wide, which blocks any future *intentional* strikethrough — a deliberate trade, and the failure message names the `\~` remedy rather than only the built file.

## In both workflows

`docs.yml` deploys on every push touching `docs/**` and had **no assertions at all** — no `needs:`, no `workflow_run` gate — so `ci.yml` could fail a merge but never a deploy. Both defects above reached production by exactly that path. `docs.yml:22` already asked for the steps to be kept in step; the two `run` bodies are byte-identical, verified by extracting both from the parsed YAML.

**Unlike #371, this PR is only half its own first test.** `ci.yml`'s `Docs build (Astro)` check below exercises the `ci.yml` copy. `docs.yml` triggers on push to `master`/`dev` only, so its copy first runs when this merges — which is the point of adding it, but worth saying plainly rather than implying both halves are proven here.

## Verified

Builds: 31 pages / 32 HTML files. A whole-tree diff shows exactly **two** HTML files changed plus the added image; `index.html` byte-identical. Each of the three defect patterns also fires in isolation.

Pending until deployed: that the image resolves over HTTP and on github.com. GitHub proxies external images through **camo, which caches** — so a broken image on the first look after merge is a cache, not a bug.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7201f03e95aa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.