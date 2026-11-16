# Issue

**Title:** [DEPENDABOT]: Bump pandas from 1.2.5 to 1.3.0

## Description

Bumps [pandas](https://github.com/pandas-dev/pandas) from 1.2.5 to 1.3.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pandas-dev/pandas/releases">pandas's releases</a>.</em></p>
<blockquote>
<h2>Pandas 1.3.0</h2>
<p>This release includes some new features, bug fixes, and performance improvements. We recommend that all users upgrade to this version.</p>
<p>See the <a href="https://pandas.pydata.org/pandas-docs/version/1.3.0/whatsnew/v1.3.0.html">full whatsnew</a> for a list of all the changes.</p>
<p>The release will be available on the defaults and conda-forge channels:</p>
<pre><code>conda install -c conda-forge pandas
</code></pre>
<p>Or via PyPI:</p>
<pre><code>python3 -m pip install --upgrade pandas
</code></pre>
<p>Please report any issues with the release on the <a href="https://github.com/pandas-dev/pandas/issues">pandas issue tracker</a>.</p>
<h2>Pandas 1.3.0rc1</h2>
<p>We are pleased to announce a release candidate for pandas 1.3.0. If all goes well, we'll release pandas 1.3.0 in about two weeks.</p>
<p>See the <a href="https://pandas.pydata.org/pandas-docs/version/1.3/whatsnew/v1.3.0.html">whatsnew</a> for a list of all the changes.</p>
<p>The release will be available on conda-forge and PyPI.</p>
<p>The release can be installed from PyPI</p>
<pre><code>python -m pip install --upgrade --pre pandas==1.3.0rc1
</code></pre>
<p>Or from conda-forge</p>
<pre><code>conda install -c conda-forge/label/pandas_rc pandas==1.3.0rc1
</code></pre>
<p>Please report any issues with the release candidate on the pandas issue tracker.</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>f00ed8f</code></a> RLS: 1.3.0</li>
<li><a href=""><code>b312d15</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42313">#42313</a>: DOC: v1.3.0 release date (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42337">#42337</a>)</li>
<li><a href=""><code>033041d</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42334">#42334</a>: PERF/REGR: restore IntervalIndex._intersection_non_unique...</li>
<li><a href=""><code>2c26ee7</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42323">#42323</a> on branch 1.3.x (BUG: <code>Styler.to_latex</code> now doesn't manipu...</li>
<li><a href=""><code>061642a</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42318">#42318</a>: PERF/REGR: symmetric_difference revert most of <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/41833">#41833</a> (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/4">#4</a>...</li>
<li><a href=""><code>f1d1367</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42317">#42317</a>: Revert &quot;REF: move shift logic from BlockManager to DataFr...</li>
<li><a href=""><code>9107f58</code></a> Auto backport of pr 42293 on 1.3.x (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42306">#42306</a>)</li>
<li><a href=""><code>538d69a</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42292">#42292</a>: REGR: ExcelWriter fails when passed kwargs (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42300">#42300</a>)</li>
<li><a href=""><code>282b76e</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/41283">#41283</a>: TYP Series and DataFrame currently type-check as hashable...</li>
<li><a href=""><code>aff6a8c</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42256">#42256</a>: CI: fewer workers on windows (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/42298">#42298</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/pandas-dev/pandas/compare/v1.2.5...v1.3.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pandas&package-manager=pip&previous-version=1.2.5&new-version=1.3.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a58808f2a9c9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.