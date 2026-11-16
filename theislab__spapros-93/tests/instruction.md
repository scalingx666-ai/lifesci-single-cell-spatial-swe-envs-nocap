# Issue

**Title:** [DEPENDABOT]: Bump pre-commit-hooks from 3.4.0 to 4.0.1

## Description

Bumps [pre-commit-hooks](https://github.com/pre-commit/pre-commit-hooks) from 3.4.0 to 4.0.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pre-commit/pre-commit-hooks/releases">pre-commit-hooks's releases</a>.</em></p>
<blockquote>
<h2>pre-commit-hooks v4.0.1</h2>
<h3>Fixes</h3>
<ul>
<li><code>check-shebang-scripts-are-executable</code> fix entry point.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/602">#602</a> issue by <a href="https://github.com/Person-93"><code>@​Person-93</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/603">#603</a> PR by <a href="https://github.com/scop"><code>@​scop</code></a>.</li>
</ul>
</li>
</ul>
<h2>pre-commit-hooks v4.0.0</h2>
<h3>Features</h3>
<ul>
<li><code>check-json</code>: report duplicate keys.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/558">#558</a> PR by <a href="https://github.com/AdityaKhursale"><code>@​AdityaKhursale</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/554">#554</a> issue by <a href="https://github.com/adamchainz"><code>@​adamchainz</code></a>.</li>
</ul>
</li>
<li><code>no-commit-to-branch</code>: add <code>main</code> to default blocked branches.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/565">#565</a> PR by <a href="https://github.com/ndevenish"><code>@​ndevenish</code></a>.</li>
</ul>
</li>
<li><code>check-case-conflict</code>: check conflicts in directory names as well.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/575">#575</a> PR by <a href="https://github.com/slsyy"><code>@​slsyy</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/70">#70</a> issue by <a href="https://github.com/andyjack"><code>@​andyjack</code></a>.</li>
</ul>
</li>
<li><code>check-vcs-permalinks</code>: forbid other branch names.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/582">#582</a> PR by <a href="https://github.com/jack1142"><code>@​jack1142</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/581">#581</a> issue by <a href="https://github.com/jack1142"><code>@​jack1142</code></a>.</li>
</ul>
</li>
<li><code>check-shebang-scripts-are-executable</code>: new hook which ensures shebang'd scripts are executable.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/545">#545</a> PR by <a href="https://github.com/scop"><code>@​scop</code></a>.</li>
</ul>
</li>
</ul>
<h3>Fixes</h3>
<ul>
<li><code>check-executables-have-shebangs</code>: Short circuit shebang lookup on windows.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/544">#544</a> PR by <a href="https://github.com/scop"><code>@​scop</code></a>.</li>
</ul>
</li>
<li><code>requirements-txt-fixer</code>: Fix comments which have indentation
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/549">#549</a> PR by <a href="https://github.com/greshilov"><code>@​greshilov</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/548">#548</a> issue by <a href="https://github.com/greshilov"><code>@​greshilov</code></a>.</li>
</ul>
</li>
<li><code>pretty-format-json</code>: write to stdout using UTF-8 encoding.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/571">#571</a> PR by <a href="https://github.com/jack1142"><code>@​jack1142</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/570">#570</a> issue by <a href="https://github.com/jack1142"><code>@​jack1142</code></a>.</li>
</ul>
</li>
<li>Use more inclusive language.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/599">#599</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
</ul>
</li>
</ul>
<h3>Breaking changes</h3>
<ul>
<li>Remove deprecated hooks: <code>flake8</code>, <code>pyflakes</code>, <code>autopep8-wrapper</code>.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/597">#597</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
</ul>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pre-commit/pre-commit-hooks/blob/master/CHANGELOG.md">pre-commit-hooks's changelog</a>.</em></p>
<blockquote>
<h1>4.0.1 - 2021-05-16</h1>
<h3>Fixes</h3>
<ul>
<li><code>check-shebang-scripts-are-executable</code> fix entry point.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/602">#602</a> issue by <a href="https://github.com/Person-93"><code>@​Person-93</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/603">#603</a> PR by <a href="https://github.com/scop"><code>@​scop</code></a>.</li>
</ul>
</li>
</ul>
<h1>4.0.0 - 2021-05-14</h1>
<h3>Features</h3>
<ul>
<li><code>check-json</code>: report duplicate keys.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/558">#558</a> PR by <a href="https://github.com/AdityaKhursale"><code>@​AdityaKhursale</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/554">#554</a> issue by <a href="https://github.com/adamchainz"><code>@​adamchainz</code></a>.</li>
</ul>
</li>
<li><code>no-commit-to-branch</code>: add <code>main</code> to default blocked branches.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/565">#565</a> PR by <a href="https://github.com/ndevenish"><code>@​ndevenish</code></a>.</li>
</ul>
</li>
<li><code>check-case-conflict</code>: check conflicts in directory names as well.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/575">#575</a> PR by <a href="https://github.com/slsyy"><code>@​slsyy</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/70">#70</a> issue by <a href="https://github.com/andyjack"><code>@​andyjack</code></a>.</li>
</ul>
</li>
<li><code>check-vcs-permalinks</code>: forbid other branch names.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/582">#582</a> PR by <a href="https://github.com/jack1142"><code>@​jack1142</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/581">#581</a> issue by <a href="https://github.com/jack1142"><code>@​jack1142</code></a>.</li>
</ul>
</li>
<li><code>check-shebang-scripts-are-executable</code>: new hook which ensures shebang'd
scripts are executable.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/545">#545</a> PR by <a href="https://github.com/scop"><code>@​scop</code></a>.</li>
</ul>
</li>
</ul>
<h3>Fixes</h3>
<ul>
<li><code>check-executables-have-shebangs</code>: Short circuit shebang lookup on windows.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/544">#544</a> PR by <a href="https://github.com/scop"><code>@​scop</code></a>.</li>
</ul>
</li>
<li><code>requirements-txt-fixer</code>: Fix comments which have indentation
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/549">#549</a> PR by <a href="https://github.com/greshilov"><code>@​greshilov</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/548">#548</a> issue by <a href="https://github.com/greshilov"><code>@​greshilov</code></a>.</li>
</ul>
</li>
<li><code>pretty-format-json</code>: write to stdout using UTF-8 encoding.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/571">#571</a> PR by <a href="https://github.com/jack1142"><code>@​jack1142</code></a>.</li>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/570">#570</a> issue by <a href="https://github.com/jack1142"><code>@​jack1142</code></a>.</li>
</ul>
</li>
<li>Use more inclusive language.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/599">#599</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
</ul>
</li>
</ul>
<h3>Breaking changes</h3>
<ul>
<li>Remove deprecated hooks: <code>flake8</code>, <code>pyflakes</code>, <code>autopep8-wrapper</code>.
<ul>
<li><a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/597">#597</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
</ul>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>38b8824</code></a> v4.0.1</li>
<li><a href=""><code>0e40c1d</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/603">#603</a> from scop/check_shebang_scripts_are_executable-entryp...</li>
<li><a href=""><code>bb4eef1</code></a> fix: check-shebang-scripts-are-executable entry point</li>
<li><a href=""><code>dd34447</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/601">#601</a> from ibLeDy/fix/check-json-hook-failing</li>
<li><a href=""><code>fed8b6d</code></a> Rename file causing <code>check-json</code> to fail</li>
<li><a href=""><code>9cc62e1</code></a> v4.0.0</li>
<li><a href=""><code>b0b1a41</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/599">#599</a> from pre-commit/all-repos_autofix_more-inclusive-lang...</li>
<li><a href=""><code>a5cf10d</code></a> Use more inclusive language</li>
<li><a href=""><code>11a996e</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pre-commit/pre-commit-hooks/issues/597">#597</a> from pre-commit/remove-deprecated</li>
<li><a href=""><code>1995abf</code></a> remove deprecated autopep8-wrapper, flake8, pyflakes</li>
<li>Additional commits viewable in <a href="https://github.com/pre-commit/pre-commit-hooks/compare/v3.4.0...v4.0.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pre-commit-hooks&package-manager=pip&previous-version=3.4.0&new-version=4.0.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bb02c1ddfc2f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.