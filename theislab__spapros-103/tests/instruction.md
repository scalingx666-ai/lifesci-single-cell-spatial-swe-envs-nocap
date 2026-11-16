# Issue

**Title:** [DEPENDABOT]: Bump black from 21.5b1 to 21.5b2

## Description

Bumps [black](https://github.com/psf/black) from 21.5b1 to 21.5b2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/psf/black/releases">black's releases</a>.</em></p>
<blockquote>
<h2>21.5b2</h2>
<h3><em>Black</em></h3>
<ul>
<li>A space is no longer inserted into empty docstrings (<a href="https://github-redirect.dependabot.com/psf/black/issues/2249">#2249</a>)</li>
<li>Fix handling of .gitignore files containing non-ASCII characters on Windows (<a href="https://github-redirect.dependabot.com/psf/black/issues/2229">#2229</a>)</li>
<li>Respect <code>.gitignore</code> files in all levels, not only <code>root/.gitignore</code> file (apply
<code>.gitignore</code> rules like <code>git</code> does) (<a href="https://github-redirect.dependabot.com/psf/black/issues/2225">#2225</a>)</li>
<li>Restored compatibility with Click 8.0 on Python 3.6 when LANG=C used (<a href="https://github-redirect.dependabot.com/psf/black/issues/2227">#2227</a>)</li>
<li>Add extra uvloop install + import support if in python env (<a href="https://github-redirect.dependabot.com/psf/black/issues/2258">#2258</a>)</li>
<li>Fix --experimental-string-processing crash when matching parens are not found (<a href="https://github-redirect.dependabot.com/psf/black/issues/2283">#2283</a>)</li>
<li>Make sure to split lines that start with a string operator (<a href="https://github-redirect.dependabot.com/psf/black/issues/2286">#2286</a>)</li>
<li>Fix regular expression that black uses to identify f-expressions (<a href="https://github-redirect.dependabot.com/psf/black/issues/2287">#2287</a>)</li>
</ul>
<h3><em>Blackd</em></h3>
<ul>
<li>Add a lower bound for the <code>aiohttp-cors</code> dependency. Only 0.4.0 or higher is
supported. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2231">#2231</a>)</li>
</ul>
<h3><em>Packaging</em></h3>
<ul>
<li>Release self-contained x86_64 MacOS binaries as part of the GitHub release pipeline
(<a href="https://github-redirect.dependabot.com/psf/black/issues/2198">#2198</a>)</li>
<li>Always build binaries with the latest available Python (<a href="https://github-redirect.dependabot.com/psf/black/issues/2260">#2260</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Add discussion of magic comments to FAQ page (<a href="https://github-redirect.dependabot.com/psf/black/issues/2272">#2272</a>)</li>
<li><code>--experimental-string-processing</code> will be enabled by default in the future (<a href="https://github-redirect.dependabot.com/psf/black/issues/2273">#2273</a>)</li>
<li>Fix typos discovered by codespell (<a href="https://github-redirect.dependabot.com/psf/black/issues/2228">#2228</a>)</li>
<li>Fix Vim plugin installation instructions. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2235">#2235</a>)</li>
<li>Add new Frequently Asked Questions page (<a href="https://github-redirect.dependabot.com/psf/black/issues/2247">#2247</a>)</li>
<li>Fix encoding + symlink issues preventing proper build on Windows (<a href="https://github-redirect.dependabot.com/psf/black/issues/2262">#2262</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/psf/black/blob/main/CHANGES.md">black's changelog</a>.</em></p>
<blockquote>
<h2>21.5b2</h2>
<h3><em>Black</em></h3>
<ul>
<li>A space is no longer inserted into empty docstrings (<a href="https://github-redirect.dependabot.com/psf/black/issues/2249">#2249</a>)</li>
<li>Fix handling of .gitignore files containing non-ASCII characters on Windows (<a href="https://github-redirect.dependabot.com/psf/black/issues/2229">#2229</a>)</li>
<li>Respect <code>.gitignore</code> files in all levels, not only <code>root/.gitignore</code> file (apply
<code>.gitignore</code> rules like <code>git</code> does) (<a href="https://github-redirect.dependabot.com/psf/black/issues/2225">#2225</a>)</li>
<li>Restored compatibility with Click 8.0 on Python 3.6 when LANG=C used (<a href="https://github-redirect.dependabot.com/psf/black/issues/2227">#2227</a>)</li>
<li>Add extra uvloop install + import support if in python env (<a href="https://github-redirect.dependabot.com/psf/black/issues/2258">#2258</a>)</li>
<li>Fix --experimental-string-processing crash when matching parens are not found (<a href="https://github-redirect.dependabot.com/psf/black/issues/2283">#2283</a>)</li>
<li>Make sure to split lines that start with a string operator (<a href="https://github-redirect.dependabot.com/psf/black/issues/2286">#2286</a>)</li>
<li>Fix regular expression that black uses to identify f-expressions (<a href="https://github-redirect.dependabot.com/psf/black/issues/2287">#2287</a>)</li>
</ul>
<h3><em>Blackd</em></h3>
<ul>
<li>Add a lower bound for the <code>aiohttp-cors</code> dependency. Only 0.4.0 or higher is
supported. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2231">#2231</a>)</li>
</ul>
<h3>Integrations</h3>
<ul>
<li>The official Black action now supports choosing what version to use, and supports the
major 3 OSes. (<a href="https://github-redirect.dependabot.com/psf/black/issues/1940">#1940</a>)</li>
</ul>
<h3>Packaging</h3>
<ul>
<li>Release self-contained x86_64 MacOS binaries as part of the GitHub release pipeline
(<a href="https://github-redirect.dependabot.com/psf/black/issues/2198">#2198</a>)</li>
<li>Always build binaries with the latest available Python (<a href="https://github-redirect.dependabot.com/psf/black/issues/2260">#2260</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Add discussion of magic comments to FAQ page (<a href="https://github-redirect.dependabot.com/psf/black/issues/2272">#2272</a>)</li>
<li><code>--experimental-string-processing</code> will be enabled by default in the future (<a href="https://github-redirect.dependabot.com/psf/black/issues/2273">#2273</a>)</li>
<li>Fix typos discovered by codespell (<a href="https://github-redirect.dependabot.com/psf/black/issues/2228">#2228</a>)</li>
<li>Fix Vim plugin installation instructions. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2235">#2235</a>)</li>
<li>Add new Frequently Asked Questions page (<a href="https://github-redirect.dependabot.com/psf/black/issues/2247">#2247</a>)</li>
<li>Fix encoding + symlink issues preventing proper build on Windows (<a href="https://github-redirect.dependabot.com/psf/black/issues/2262">#2262</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/psf/black/commits">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=black&package-manager=pip&previous-version=21.5b1&new-version=21.5b2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5dcc3e861b04`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.