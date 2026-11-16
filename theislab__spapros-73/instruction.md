# Issue

**Title:** [DEPENDABOT]: Bump pandas from 1.2.3 to 1.2.4

## Description

[//]: # (dependabot-start)
⚠️  **Dependabot is rebasing this PR** ⚠️

If you make any changes to it yourself then they will take precedence over the rebase.

---

[//]: # (dependabot-end)

Bumps [pandas](https://github.com/pandas-dev/pandas) from 1.2.3 to 1.2.4.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pandas-dev/pandas/releases">pandas's releases</a>.</em></p>
<blockquote>
<h2>Pandas 1.2.4</h2>
<p>This is a patch release in the 1.2.x series and includes some regression fixes. We recommend that all users upgrade to this version.</p>
<p>See the <a href="https://pandas.pydata.org/pandas-docs/version/1.2.4/whatsnew/v1.2.4.html">full whatsnew</a> for a list of all the changes.</p>
<p>The release will be available on the defaults and conda-forge channels:</p>
<pre><code>conda install pandas
</code></pre>
<p>Or via PyPI:</p>
<pre><code>python3 -m pip install --upgrade pandas
</code></pre>
<p>Please report any issues with the release on the <a href="https://github.com/pandas-dev/pandas/issues">pandas issue tracker</a>.</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2cb9652</code></a> RLS: 1.2.4</li>
<li><a href=""><code>0428542</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40878">#40878</a>: REGR: ufunc with DataFrame input not passing all kwargs (...</li>
<li><a href=""><code>57dd3d2</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40880">#40880</a>: DOC: 1.2.4 release date (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40894">#40894</a>)</li>
<li><a href=""><code>7b1803c</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40877">#40877</a> on branch 1.2.x (Skipt failing tests for numpy dev) (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40882">#40882</a>)</li>
<li><a href=""><code>3fae915</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40850">#40850</a>: REGR: object column repr not respecting float format (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40">#40</a>...</li>
<li><a href=""><code>8493555</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40407">#40407</a>: DOC: remove pin for pydata-sphinx-theme + update for late...</li>
<li><a href=""><code>a2cbc03</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/38574">#38574</a>: TST: fix some mpl warnings (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40801">#40801</a>)</li>
<li><a href=""><code>c8c57a8</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40723">#40723</a>: BUG: fix comparison of NaT with numpy array (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40734">#40734</a>)</li>
<li><a href=""><code>fd2a85a</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40718">#40718</a>: COMPAT: matplotlib 3.4.0 (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40739">#40739</a>)</li>
<li><a href=""><code>114e0d9</code></a> Backport PR <a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40604">#40604</a>: REGR: replace with multivalued regex raising (<a href="https://github-redirect.dependabot.com/pandas-dev/pandas/issues/40648">#40648</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/pandas-dev/pandas/compare/v1.2.3...v1.2.4">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pandas&package-manager=pip&previous-version=1.2.3&new-version=1.2.4)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a155394e92b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.