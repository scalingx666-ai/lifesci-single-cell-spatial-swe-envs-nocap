# Issue

**Title:** [DEPENDABOT]: Bump sphinx-rtd-theme from 1.3.0 to 2.0.0

## Description

Bumps [sphinx-rtd-theme](https://github.com/readthedocs/sphinx_rtd_theme) from 1.3.0 to 2.0.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/readthedocs/sphinx_rtd_theme/blob/master/docs/changelog.rst">sphinx-rtd-theme's changelog</a>.</em></p>
<blockquote>
<h1>2.0.0</h1>
<h2>Added</h2>
<ul>
<li>Support for Sphinx versions <code>6.x</code> and <code>7.x</code></li>
<li>Support for docutils <code>&lt;=0.20</code></li>
</ul>
<h2>Deprecations</h2>
<ul>
<li>The HTML4 writer is now officially deprecated. An error will be thrown if your
project configuration still uses the HTML4 writer.</li>
<li>Support for Sphinx versions &lt; 5.0 was removed.</li>
<li>In addition, our supported dependencies will match the dependencies from our
lowest supported Sphinx release, version 5.0: Python &gt;= 3.6 and docutils &gt; 0.14 and &lt; 0.19</li>
</ul>
<p>.. _release-1.3.0:</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7c9b1b5</code></a> Release 2.0 final (<a href="">#1544</a>)</li>
<li><a href=""><code>c104410</code></a> Bump for next potential release, 2.0.0rc5 (<a href="">#1539</a>)</li>
<li><a href=""><code>53ca116</code></a> Release 2.0.0rc4 (<a href="">#1538</a>)</li>
<li><a href=""><code>4498e97</code></a> Fix AttributeError when one of <code>css_files</code> is a string (<a href="">#1537</a>)</li>
<li><a href=""><code>84aea9b</code></a> Increment for next potential release (<a href="">#1536</a>)</li>
<li><a href=""><code>febde39</code></a> Release 2.0.0rc3 (<a href="">#1535</a>)</li>
<li><a href=""><code>32310a8</code></a> Fix <a href="">#1522</a>: fix <code>'str' object has no attribute 'attributes'</code> (<a href="">#1528</a>)</li>
<li><a href=""><code>8ce23ce</code></a> Version bump for 2.0rc3 development (<a href="">#1521</a>)</li>
<li><a href=""><code>46f5307</code></a> Release 2.0rc2 (<a href="">#1520</a>)</li>
<li><a href=""><code>5838e6a</code></a> Add support for <code>docutils==0.20.x</code> (<a href="">#1517</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/readthedocs/sphinx_rtd_theme/compare/1.3.0...2.0.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sphinx-rtd-theme&package-manager=pip&previous-version=1.3.0&new-version=2.0.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ecb19f0544f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.