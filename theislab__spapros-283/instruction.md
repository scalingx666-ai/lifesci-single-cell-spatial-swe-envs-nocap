# Issue

**Title:** [DEPENDABOT]: Bump sphinx-rtd-theme from 0.5.2 to 1.3.0

## Description

Bumps [sphinx-rtd-theme](https://github.com/readthedocs/sphinx_rtd_theme) from 0.5.2 to 1.3.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/readthedocs/sphinx_rtd_theme/blob/master/docs/changelog.rst">sphinx-rtd-theme's changelog</a>.</em></p>
<blockquote>
<h1>1.3.0</h1>
<h2>Added</h2>
<ul>
<li>Relaxed requirements to include Sphinx release <code>7.0</code></li>
</ul>
<p>.. _release-1.2.2:</p>
<h1>1.2.2</h1>
<h2>Fixes</h2>
<ul>
<li>Require <code>sphinxcontrib-jquery&gt;=4,&lt;5</code> (<a href="">#1446</a>)</li>
</ul>
<h2>Added</h2>
<ul>
<li>Styling for <code>:menuselection:</code> (<a href="">#1426</a>)</li>
</ul>
<p>.. _release-1.2.1:</p>
<h1>1.2.1</h1>
<h2>Fixes</h2>
<ul>
<li>Load jQuery correctly when using latest sphinxcontrib-jquery release (<a href="">#1448</a>)</li>
</ul>
<p>.. _release-1.2.0:</p>
<h1>1.2.0</h1>
<h2>Dependency changes</h2>
<ul>
<li>docutils 0.18 is supported. (<a href="">#1381</a>)</li>
<li>Sphinx 6 support added</li>
<li>Added <code>sphinxcontrib-jquery</code> as a dependency (<a href="">#1385</a> <a href="">#1421</a>)</li>
<li>Python 3.11 is officially supported and tested. (<a href="">#1395</a>)</li>
<li>Python 3.4 and 3.5 are officially not supported (<a href="">#1395</a>)</li>
</ul>
<p>Changes</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>15ed4de</code></a> Release 1.3.0 (<a href="">#1509</a>)</li>
<li><a href=""><code>b583358</code></a> 1.3.0rc2 (<a href="">#1495</a>)</li>
<li><a href=""><code>775bca4</code></a> Release 1.3.0rc1 (<a href="">#1494</a>)</li>
<li><a href=""><code>04f85fc</code></a> Add Sphinx 7 support (<a href="">#1464</a>)</li>
<li><a href=""><code>9899ee4</code></a> Release 1.2.2 (<a href="">#1484</a>)</li>
<li><a href=""><code>2442ab9</code></a> Remove version logic on sphinxcontrib-jquery, require &gt;=4,&lt;5 (<a href="">#1446</a>)</li>
<li><a href=""><code>cd6b429</code></a> :menuselection: style (<a href="">#1426</a>)</li>
<li><a href=""><code>2107797</code></a> Contributing updates (<a href="">#1478</a>)</li>
<li><a href=""><code>72691f5</code></a> Release 1.2.1 (<a href="">#1474</a>)</li>
<li><a href=""><code>d836ff7</code></a> Docs: Typo in recommended pinning (<a href="">#1476</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/readthedocs/sphinx_rtd_theme/compare/0.5.2...1.3.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sphinx-rtd-theme&package-manager=pip&previous-version=0.5.2&new-version=1.3.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `176fd6efcdc9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.