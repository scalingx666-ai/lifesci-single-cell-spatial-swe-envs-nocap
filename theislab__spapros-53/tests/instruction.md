# Issue

**Title:** [DEPENDABOT]: Bump pytest from 6.2.2 to 6.2.3

## Description

Bumps [pytest](https://github.com/pytest-dev/pytest) from 6.2.2 to 6.2.3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pytest-dev/pytest/releases">pytest's releases</a>.</em></p>
<blockquote>
<h2>6.2.3</h2>
<h1>pytest 6.2.3 (2021-04-03)</h1>
<h2>Bug Fixes</h2>
<ul>
<li>
<p><a href="https://github-redirect.dependabot.com/pytest-dev/pytest/issues/8414">#8414</a>: pytest used to create directories under <code>/tmp</code> with world-readable
permissions. This means that any user in the system was able to read
information written by tests in temporary directories (such as those created by
the <code>tmp_path</code>/<code>tmpdir</code> fixture). Now the directories are created with
private permissions.</p>
<p>pytest used silenty use a pre-existing <code>/tmp/pytest-of-&lt;username&gt;</code> directory,
even if owned by another user. This means another user could pre-create such a
directory and gain control of another user's temporary directory. Now such a
condition results in an error.</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>3a2fd96</code></a> Prepare release version 6.2.3</li>
<li><a href=""><code>138b19a</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pytest-dev/pytest/issues/8517">#8517</a> from bluetech/backport-mktmp</li>
<li><a href=""><code>822686e</code></a> tmpdir: prevent using a non-private root temp directory</li>
<li><a href=""><code>9dc54f7</code></a> tmpdir: fix temporary directories created with world-readable permissions</li>
<li><a href=""><code>93dbae2</code></a> pathlib: inline ensure_reset_dir()</li>
<li><a href=""><code>02fdbe2</code></a> pathlib: remove useless temporary variable</li>
<li><a href=""><code>12e7db8</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pytest-dev/pytest/issues/8285">#8285</a> from nicoddemus/backport-8280</li>
<li><a href=""><code>56e4392</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pytest-dev/pytest/issues/8280">#8280</a> from xuhdev/module</li>
<li><a href=""><code>8220eca</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pytest-dev/pytest/issues/8275">#8275</a> from pytest-dev/release-6.2.2</li>
<li>See full diff in <a href="https://github.com/pytest-dev/pytest/compare/6.2.2...6.2.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pytest&package-manager=pip&previous-version=6.2.2&new-version=6.2.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b055c26b957e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.