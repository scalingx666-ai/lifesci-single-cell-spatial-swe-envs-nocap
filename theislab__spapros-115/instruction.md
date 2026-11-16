# Issue

**Title:** [DEPENDABOT]: Bump black from 21.5b2 to 21.6b0

## Description

Bumps [black](https://github.com/psf/black) from 21.5b2 to 21.6b0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/psf/black/releases">black's releases</a>.</em></p>
<blockquote>
<h2>21.6b0</h2>
<h2><em>Black</em></h2>
<ul>
<li>Fix failure caused by <code>fmt: skip</code> and indentation (<a href="https://github-redirect.dependabot.com/psf/black/issues/2281">#2281</a>)</li>
<li>Account for += assignment when deciding whether to split string (<a href="https://github-redirect.dependabot.com/psf/black/issues/2312">#2312</a>)</li>
<li>Correct max string length calculation when there are string operators (<a href="https://github-redirect.dependabot.com/psf/black/issues/2292">#2292</a>)</li>
<li>Fixed option usage when using the <code>--code</code> flag (<a href="https://github-redirect.dependabot.com/psf/black/issues/2259">#2259</a>)</li>
<li>Do not call <code>uvloop.install()</code> when <em>Black</em> is used as a library (<a href="https://github-redirect.dependabot.com/psf/black/issues/2303">#2303</a>)</li>
<li>Added <code>--required-version</code> option to require a specific version to be running (<a href="https://github-redirect.dependabot.com/psf/black/issues/2300">#2300</a>)</li>
<li>Fix incorrect custom breakpoint indices when string group contains fake f-strings
(<a href="https://github-redirect.dependabot.com/psf/black/issues/2311">#2311</a>)</li>
<li>Fix regression where <code>R</code> prefixes would be lowercased for docstrings (<a href="https://github-redirect.dependabot.com/psf/black/issues/2285">#2285</a>)</li>
<li>Fix handling of named escapes (<code>\N{...}</code>) when <code>--experimental-string-processing</code> is
used (<a href="https://github-redirect.dependabot.com/psf/black/issues/2319">#2319</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/psf/black/blob/main/CHANGES.md">black's changelog</a>.</em></p>
<blockquote>
<h2>21.6b0</h2>
<h3><em>Black</em></h3>
<ul>
<li>Fix failure caused by <code>fmt: skip</code> and indentation (<a href="https://github-redirect.dependabot.com/psf/black/issues/2281">#2281</a>)</li>
<li>Account for += assignment when deciding whether to split string (<a href="https://github-redirect.dependabot.com/psf/black/issues/2312">#2312</a>)</li>
<li>Correct max string length calculation when there are string operators (<a href="https://github-redirect.dependabot.com/psf/black/issues/2292">#2292</a>)</li>
<li>Fixed option usage when using the <code>--code</code> flag (<a href="https://github-redirect.dependabot.com/psf/black/issues/2259">#2259</a>)</li>
<li>Do not call <code>uvloop.install()</code> when <em>Black</em> is used as a library (<a href="https://github-redirect.dependabot.com/psf/black/issues/2303">#2303</a>)</li>
<li>Added <code>--required-version</code> option to require a specific version to be running (<a href="https://github-redirect.dependabot.com/psf/black/issues/2300">#2300</a>)</li>
<li>Fix incorrect custom breakpoint indices when string group contains fake f-strings
(<a href="https://github-redirect.dependabot.com/psf/black/issues/2311">#2311</a>)</li>
<li>Fix regression where <code>R</code> prefixes would be lowercased for docstrings (<a href="https://github-redirect.dependabot.com/psf/black/issues/2285">#2285</a>)</li>
<li>Fix handling of named escapes (<code>\N{...}</code>) when <code>--experimental-string-processing</code> is
used (<a href="https://github-redirect.dependabot.com/psf/black/issues/2319">#2319</a>)</li>
</ul>
<h3>Integrations</h3>
<ul>
<li>The vim plugin now searches upwards from the directory containing the current buffer
instead of the current working directory for pyproject.toml. (<a href="https://github-redirect.dependabot.com/psf/black/issues/1871">#1871</a>)</li>
</ul>
<h3>Integrations</h3>
<ul>
<li>The vim plugin now reads the correct string normalization option in pyproject.toml
(<a href="https://github-redirect.dependabot.com/psf/black/issues/1869">#1869</a>)</li>
<li>The vim plugin no longer crashes Black when there's boolean values in pyproject.toml
(<a href="https://github-redirect.dependabot.com/psf/black/issues/1869">#1869</a>)</li>
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

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=black&package-manager=pip&previous-version=21.5b2&new-version=21.6b0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3509362b5a97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.