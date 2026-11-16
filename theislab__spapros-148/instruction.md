# Issue

**Title:** [DEPENDABOT]: Bump black from 21.6b0 to 21.7b0

## Description

Bumps [black](https://github.com/psf/black) from 21.6b0 to 21.7b0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/psf/black/releases">black's releases</a>.</em></p>
<blockquote>
<h2>21.7b0</h2>
<h3><em>Black</em></h3>
<ul>
<li>Configuration files using TOML features higher than spec v0.5.0 are now supported
(<a href="https://github-redirect.dependabot.com/psf/black/issues/2301">#2301</a>)</li>
<li>Add primer support and test for code piped into black via STDIN (<a href="https://github-redirect.dependabot.com/psf/black/issues/2315">#2315</a>)</li>
<li>Fix internal error when <code>FORCE_OPTIONAL_PARENTHESES</code> feature is enabled (<a href="https://github-redirect.dependabot.com/psf/black/issues/2332">#2332</a>)</li>
<li>Accept empty stdin (<a href="https://github-redirect.dependabot.com/psf/black/issues/2346">#2346</a>)</li>
<li>Provide a more useful error when parsing fails during AST safety checks (<a href="https://github-redirect.dependabot.com/psf/black/issues/2304">#2304</a>)</li>
</ul>
<h3>Docker</h3>
<ul>
<li>Add new <code>latest_release</code> tag automation to follow latest black release on docker
images (<a href="https://github-redirect.dependabot.com/psf/black/issues/2374">#2374</a>)</li>
</ul>
<h3>Integrations</h3>
<ul>
<li>The vim plugin now searches upwards from the directory containing the current buffer
instead of the current working directory for pyproject.toml. (<a href="https://github-redirect.dependabot.com/psf/black/issues/1871">#1871</a>)</li>
<li>The vim plugin now reads the correct string normalization option in pyproject.toml
(<a href="https://github-redirect.dependabot.com/psf/black/issues/1869">#1869</a>)</li>
<li>The vim plugin no longer crashes Black when there's boolean values in pyproject.toml
(<a href="https://github-redirect.dependabot.com/psf/black/issues/1869">#1869</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/psf/black/blob/main/CHANGES.md">black's changelog</a>.</em></p>
<blockquote>
<h2>21.7b0</h2>
<h3><em>Black</em></h3>
<ul>
<li>Configuration files using TOML features higher than spec v0.5.0 are now supported
(<a href="https://github-redirect.dependabot.com/psf/black/issues/2301">#2301</a>)</li>
<li>Add primer support and test for code piped into black via STDIN (<a href="https://github-redirect.dependabot.com/psf/black/issues/2315">#2315</a>)</li>
<li>Fix internal error when <code>FORCE_OPTIONAL_PARENTHESES</code> feature is enabled (<a href="https://github-redirect.dependabot.com/psf/black/issues/2332">#2332</a>)</li>
<li>Accept empty stdin (<a href="https://github-redirect.dependabot.com/psf/black/issues/2346">#2346</a>)</li>
<li>Provide a more useful error when parsing fails during AST safety checks (<a href="https://github-redirect.dependabot.com/psf/black/issues/2304">#2304</a>)</li>
</ul>
<h3>Docker</h3>
<ul>
<li>Add new <code>latest_release</code> tag automation to follow latest black release on docker
images (<a href="https://github-redirect.dependabot.com/psf/black/issues/2374">#2374</a>)</li>
</ul>
<h3>Integrations</h3>
<ul>
<li>The vim plugin now searches upwards from the directory containing the current buffer
instead of the current working directory for pyproject.toml. (<a href="https://github-redirect.dependabot.com/psf/black/issues/1871">#1871</a>)</li>
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

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=black&package-manager=pip&previous-version=21.6b0&new-version=21.7b0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0ebfc1dcd05`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.