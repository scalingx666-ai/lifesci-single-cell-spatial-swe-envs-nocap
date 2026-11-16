# Issue

**Title:** [DEPENDABOT]: Bump xdoctest from 0.15.4 to 0.15.5

## Description

Bumps [xdoctest](https://github.com/Erotemic/xdoctest) from 0.15.4 to 0.15.5.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/Erotemic/xdoctest/releases">xdoctest's releases</a>.</em></p>
<blockquote>
<h2>Version 0.15.5 - Released 2021-06-27</h2>
<h3>Changed</h3>
<ul>
<li>Better message when a pytest skip or exit-test-exception occurs</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Suppressed warning about using internal <code>FixtureRequest</code></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/Erotemic/xdoctest/blob/master/CHANGELOG.md">xdoctest's changelog</a>.</em></p>
<blockquote>
<h2>Version 0.15.5 - Unreleased</h2>
<h3>Changed</h3>
<ul>
<li>Better message when a pytest skip or exit-test-exception occurs</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Suppressed warning about using internal <code>FixtureRequest</code></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ddaad20</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/Erotemic/xdoctest/issues/96">#96</a> from Erotemic/dev/0.15.5</li>
<li><a href=""><code>7609992</code></a> Attempt to fix pytest version warning</li>
<li><a href=""><code>03ff9de</code></a> Try and fix warning again</li>
<li><a href=""><code>38c5243</code></a> Fixed CCI 3.6 test which actually ran 3.5</li>
<li><a href=""><code>b241915</code></a> wip</li>
<li><a href=""><code>2fb1353</code></a> Update pytest in requirements</li>
<li><a href=""><code>a9abf77</code></a> wip</li>
<li><a href=""><code>21aed84</code></a> wip</li>
<li><a href=""><code>c854b08</code></a> wip</li>
<li><a href=""><code>76e21a5</code></a> wip</li>
<li>Additional commits viewable in <a href="https://github.com/Erotemic/xdoctest/compare/0.15.4...0.15.5">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=xdoctest&package-manager=pip&previous-version=0.15.4&new-version=0.15.5)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e93366b43911`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.