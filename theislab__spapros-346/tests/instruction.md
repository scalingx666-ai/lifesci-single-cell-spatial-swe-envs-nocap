# Issue

**Title:** [DEPENDABOT]: Bump pre-commit-hooks from 4.5.0 to 4.6.0

## Description

Bumps [pre-commit-hooks](https://github.com/pre-commit/pre-commit-hooks) from 4.5.0 to 4.6.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pre-commit/pre-commit-hooks/releases">pre-commit-hooks's releases</a>.</em></p>
<blockquote>
<h2>pre-commit-hooks v4.6.0</h2>
<h3>Features</h3>
<ul>
<li><code>requirements-txt-fixer</code>: remove duplicate packages.
<ul>
<li><a href="">#1014</a> PR by <a href="https://github.com/vhoulbreque-withings"><code>@​vhoulbreque-withings</code></a>.</li>
<li><a href="">#960</a> issue <a href="https://github.com/csibe17"><code>@​csibe17</code></a>.</li>
</ul>
</li>
</ul>
<h3>Migrating</h3>
<ul>
<li><code>fix-encoding-pragma</code>: deprecated -- will be removed in 5.0.0.  use
<a href="https://github.com/asottile/pyupgrade">pyupgrade</a> or some other tool.
<ul>
<li><a href="">#1033</a> PR by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
<li><a href="">#1032</a> issue by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
</ul>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pre-commit/pre-commit-hooks/blob/main/CHANGELOG.md">pre-commit-hooks's changelog</a>.</em></p>
<blockquote>
<h1>4.6.0 - 2024-04-06</h1>
<h3>Features</h3>
<ul>
<li><code>requirements-txt-fixer</code>: remove duplicate packages.
<ul>
<li><a href="">#1014</a> PR by <a href="https://github.com/vhoulbreque-withings"><code>@​vhoulbreque-withings</code></a>.</li>
<li><a href="">#960</a> issue <a href="https://github.com/csibe17"><code>@​csibe17</code></a>.</li>
</ul>
</li>
</ul>
<h3>Migrating</h3>
<ul>
<li><code>fix-encoding-pragma</code>: deprecated -- will be removed in 5.0.0.  use
<a href="https://github.com/asottile/pyupgrade">pyupgrade</a> or some other tool.
<ul>
<li><a href="">#1033</a> PR by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
<li><a href="">#1032</a> issue by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
</ul>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2c9f875</code></a> v4.6.0</li>
<li><a href=""><code>d87a28b</code></a> Merge pull request <a href="">#1033</a> from pre-commit/fix-encoding-pragma</li>
<li><a href=""><code>cef973f</code></a> Add deprecation messaging for <code>fix-encoding-pragma</code></li>
<li><a href=""><code>c8715b7</code></a> Merge pull request <a href="">#1028</a> from pre-commit/pre-commit-ci-update-config</li>
<li><a href=""><code>41912f6</code></a> [pre-commit.ci] pre-commit autoupdate</li>
<li><a href=""><code>6afc574</code></a> Merge pull request <a href="">#1027</a> from pre-commit/pre-commit-ci-update-config</li>
<li><a href=""><code>6880fa1</code></a> [pre-commit.ci] pre-commit autoupdate</li>
<li><a href=""><code>2d94897</code></a> Merge pull request <a href="">#1024</a> from pre-commit/pre-commit-ci-update-config</li>
<li><a href=""><code>bda540f</code></a> [pre-commit.ci] pre-commit autoupdate</li>
<li><a href=""><code>aae27b8</code></a> Merge pull request <a href="">#1014</a> from vhoulbreque-withings/960-fix-requirements-txt-f...</li>
<li>Additional commits viewable in <a href="https://github.com/pre-commit/pre-commit-hooks/compare/v4.5.0...v4.6.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pre-commit-hooks&package-manager=pip&previous-version=4.5.0&new-version=4.6.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1453a49ef610`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.