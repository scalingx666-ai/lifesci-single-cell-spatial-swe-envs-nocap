# Issue

**Title:** [DEPENDABOT]: Bump pep8-naming from 0.11.1 to 0.12.0

## Description

Bumps [pep8-naming](https://github.com/PyCQA/pep8-naming) from 0.11.1 to 0.12.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/PyCQA/pep8-naming/blob/master/CHANGELOG.rst">pep8-naming's changelog</a>.</em></p>
<blockquote>
<h2>0.12.0 - 2021-07-06</h2>
<ul>
<li>
<p>flake8 3.9.1 or later is now required.</p>
</li>
<li>
<p>N818 checks exception class names for an &quot;Error&quot; suffix (disabled by default).</p>
</li>
<li>
<p><code>asyncSetUp</code> and <code>asyncTearDown</code> are now exempted by default.</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>60e43bb</code></a> Prepare the 0.12.0 release (<a href="https://github-redirect.dependabot.com/PyCQA/pep8-naming/issues/172">#172</a>)</li>
<li><a href=""><code>f289a72</code></a> Exempt asyncSetUp and asyncTearDown, just like setUp and tearDown (<a href="https://github-redirect.dependabot.com/PyCQA/pep8-naming/issues/170">#170</a>)</li>
<li><a href=""><code>2db856d</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/PyCQA/pep8-naming/issues/166">#166</a> from jparise/README-N814-N817</li>
<li><a href=""><code>35c3334</code></a> Reference N817 from N814, and vice-versa</li>
<li><a href=""><code>bee559c</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/PyCQA/pep8-naming/issues/157">#157</a> from ecolell/exception-names</li>
<li><a href=""><code>6d62db8</code></a> Improve tox call to include an empty list for extended-default-ignore.</li>
<li><a href=""><code>0117e40</code></a> Set requirement flake8 &gt;= 3.9.1</li>
<li><a href=""><code>b562e5a</code></a> Make N818 ignored by default.</li>
<li><a href=""><code>2430287</code></a> Reduce complexity of a comparison with an 'endswith' method call.</li>
<li><a href=""><code>eb50e59</code></a> Rename class_definition as is_class_definition to keep the name consistency.</li>
<li>Additional commits viewable in <a href="https://github.com/PyCQA/pep8-naming/compare/0.11.1...0.12.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pep8-naming&package-manager=pip&previous-version=0.11.1&new-version=0.12.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d86cc7130847`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.