# Issue

**Title:** chore(deps): bump https://github.com/pre-commit/pre-commit-hooks from v4.2.0 to 6.0.0

## Description

Bumps [https://github.com/pre-commit/pre-commit-hooks](https://github.com/pre-commit/pre-commit-hooks) from v4.2.0 to 6.0.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pre-commit/pre-commit-hooks/releases">https://github.com/pre-commit/pre-commit-hooks's releases</a>.</em></p>
<blockquote>
<h2>pre-commit-hooks v6.0.0</h2>
<h2>Fixes</h2>
<ul>
<li><code>check-shebang-scripts-are-executable</code>: improve error message.
<ul>
<li><a href="">#1115</a> PR by <a href="https://github.com/homebysix"><code>@​homebysix</code></a>.</li>
</ul>
</li>
</ul>
<h2>Migrating</h2>
<ul>
<li>now requires python &gt;= 3.9.
<ul>
<li><a href="">#1098</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
</ul>
</li>
<li><code>file-contents-sorter</code>: disallow <code>--unique</code> and <code>--ignore-case</code> at the same
time.
<ul>
<li><a href="">#1095</a> PR by <a href="https://github.com/nemacysts"><code>@​nemacysts</code></a>.</li>
<li><a href="">#794</a> issue by <a href="https://github.com/teksturi"><code>@​teksturi</code></a>.</li>
</ul>
</li>
<li>Removed <code>check-byte-order-marker</code> and <code>fix-encoding-pragma</code>.
<ul>
<li><code>check-byte-order-marker</code>: migrate to <code>fix-byte-order-marker</code>.</li>
<li><code>fix-encoding-pragma</code>: migrate to <code>pyupgrade</code>.</li>
<li><a href="">#1034</a> PR by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
<li><a href="">#1032</a> issue by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
<li><a href="">#522</a> PR by <a href="https://github.com/jgowdy"><code>@​jgowdy</code></a>.</li>
</ul>
</li>
</ul>
<h2>pre-commit-hooks v5.0.0</h2>
<h3>Features</h3>
<ul>
<li><code>requirements-txt-fixer</code>: also remove <code>pkg_resources==...</code>.
<ul>
<li><a href="">#850</a> PR by <a href="https://github.com/ericfrederich"><code>@​ericfrederich</code></a>.</li>
<li><a href="">#1030</a> issue by <a href="https://github.com/ericfrederich"><code>@​ericfrederich</code></a>.</li>
</ul>
</li>
<li><code>check-illegal-windows-names</code>: new hook!
<ul>
<li><a href="">#1044</a> PR by <a href="https://github.com/ericfrederich"><code>@​ericfrederich</code></a>.</li>
<li><a href="">#589</a> issue by <a href="https://github.com/ericfrederich"><code>@​ericfrederich</code></a>.</li>
<li><a href="">#1049</a> PR by <a href="https://github.com/Jeffrey-Lim"><code>@​Jeffrey-Lim</code></a>.</li>
</ul>
</li>
<li><code>pretty-format-json</code>: continue processing even if a file has a json error.
<ul>
<li><a href="">#1039</a> PR by <a href="https://github.com/amarvin"><code>@​amarvin</code></a>.</li>
<li><a href="">#1038</a> issue by <a href="https://github.com/amarvin"><code>@​amarvin</code></a>.</li>
</ul>
</li>
</ul>
<h3>Fixes</h3>
<ul>
<li><code>destroyed-symlinks</code>: set <code>stages</code> to <code>[pre-commit, pre-push, manual]</code>
<ul>
<li>PR <a href="">#1085</a> by <a href="https://github.com/AdrianDC"><code>@​AdrianDC</code></a>.</li>
</ul>
</li>
</ul>
<h3>Migrating</h3>
<ul>
<li>pre-commit-hooks now requires <code>pre-commit&gt;=3.2.0</code>.</li>
<li>use non-deprecated names for <code>stages</code>.
<ul>
<li><a href="">#1093</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
</ul>
</li>
</ul>
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
<li><code>fix-encoding-pragma</code>: deprecated -- will be removed in 5.0.0.  use</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pre-commit/pre-commit-hooks/blob/main/CHANGELOG.md">https://github.com/pre-commit/pre-commit-hooks's changelog</a>.</em></p>
<blockquote>
<h1>6.0.0 - 2025-08-09</h1>
<h2>Fixes</h2>
<ul>
<li><code>check-shebang-scripts-are-executable</code>: improve error message.
<ul>
<li><a href="">#1115</a> PR by <a href="https://github.com/homebysix"><code>@​homebysix</code></a>.</li>
</ul>
</li>
</ul>
<h2>Migrating</h2>
<ul>
<li>now requires python &gt;= 3.9.
<ul>
<li><a href="">#1098</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
</ul>
</li>
<li><code>file-contents-sorter</code>: disallow <code>--unique</code> and <code>--ignore-case</code> at the same
time.
<ul>
<li><a href="">#1095</a> PR by <a href="https://github.com/nemacysts"><code>@​nemacysts</code></a>.</li>
<li><a href="">#794</a> issue by <a href="https://github.com/teksturi"><code>@​teksturi</code></a>.</li>
</ul>
</li>
<li>Removed <code>check-byte-order-marker</code> and <code>fix-encoding-pragma</code>.
<ul>
<li><code>check-byte-order-marker</code>: migrate to <code>fix-byte-order-marker</code>.</li>
<li><code>fix-encoding-pragma</code>: migrate to <code>pyupgrade</code>.</li>
<li><a href="">#1034</a> PR by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
<li><a href="">#1032</a> issue by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
<li><a href="">#522</a> PR by <a href="https://github.com/jgowdy"><code>@​jgowdy</code></a>.</li>
</ul>
</li>
</ul>
<h1>5.0.0 - 2024-10-05</h1>
<h3>Features</h3>
<ul>
<li><code>requirements-txt-fixer</code>: also remove <code>pkg_resources==...</code>.
<ul>
<li><a href="">#850</a> PR by <a href="https://github.com/ericfrederich"><code>@​ericfrederich</code></a>.</li>
<li><a href="">#1030</a> issue by <a href="https://github.com/ericfrederich"><code>@​ericfrederich</code></a>.</li>
</ul>
</li>
<li><code>check-illegal-windows-names</code>: new hook!
<ul>
<li><a href="">#1044</a> PR by <a href="https://github.com/ericfrederich"><code>@​ericfrederich</code></a>.</li>
<li><a href="">#589</a> issue by <a href="https://github.com/ericfrederich"><code>@​ericfrederich</code></a>.</li>
<li><a href="">#1049</a> PR by <a href="https://github.com/Jeffrey-Lim"><code>@​Jeffrey-Lim</code></a>.</li>
</ul>
</li>
<li><code>pretty-format-json</code>: continue processing even if a file has a json error.
<ul>
<li><a href="">#1039</a> PR by <a href="https://github.com/amarvin"><code>@​amarvin</code></a>.</li>
<li><a href="">#1038</a> issue by <a href="https://github.com/amarvin"><code>@​amarvin</code></a>.</li>
</ul>
</li>
</ul>
<h3>Fixes</h3>
<ul>
<li><code>destroyed-symlinks</code>: set <code>stages</code> to <code>[pre-commit, pre-push, manual]</code>
<ul>
<li>PR <a href="">#1085</a> by <a href="https://github.com/AdrianDC"><code>@​AdrianDC</code></a>.</li>
</ul>
</li>
</ul>
<h3>Migrating</h3>
<ul>
<li>pre-commit-hooks now requires <code>pre-commit&gt;=3.2.0</code>.</li>
<li>use non-deprecated names for <code>stages</code>.
<ul>
<li><a href="">#1093</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
</ul>
</li>
</ul>
<h1>4.6.0 - 2024-04-06</h1>
<h3>Features</h3>
<ul>
<li><code>requirements-txt-fixer</code>: remove duplicate packages.</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>3e8a870</code></a> v6.0.0</li>
<li><a href=""><code>a8f8651</code></a> Merge pull request <a href="">#1185</a> from pre-commit/pre-commit-ci-update-config</li>
<li><a href=""><code>1acd88e</code></a> [pre-commit.ci] pre-commit autoupdate</li>
<li><a href=""><code>1450343</code></a> Merge pull request <a href="">#1182</a> from pre-commit/pre-commit-ci-update-config</li>
<li><a href=""><code>b554d0a</code></a> [pre-commit.ci] pre-commit autoupdate</li>
<li><a href=""><code>582b9c6</code></a> Merge pull request <a href="">#1174</a> from pre-commit/pre-commit-ci-update-config</li>
<li><a href=""><code>84f8a9d</code></a> [pre-commit.ci] pre-commit autoupdate</li>
<li><a href=""><code>ec458dc</code></a> Merge pull request <a href="">#1166</a> from pre-commit/pre-commit-ci-update-config</li>
<li><a href=""><code>1ea82df</code></a> [pre-commit.ci] pre-commit autoupdate</li>
<li><a href=""><code>540cd64</code></a> Merge pull request <a href="">#1164</a> from pre-commit/pre-commit-ci-update-config</li>
<li>Additional commits viewable in <a href="https://github.com/pre-commit/pre-commit-hooks/compare/v4.2.0...v6.0.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=https://github.com/pre-commit/pre-commit-hooks&package-manager=pre_commit&previous-version=v4.2.0&new-version=6.0.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `87f81caf571b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.