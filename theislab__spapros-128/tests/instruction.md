# Issue

**Title:** [DEPENDABOT]: Bump sphinx from 4.0.2 to 4.0.3

## Description

Bumps [sphinx](https://github.com/sphinx-doc/sphinx) from 4.0.2 to 4.0.3.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/blob/4.x/CHANGES">sphinx's changelog</a>.</em></p>
<blockquote>
<h1>Release 4.0.3 (released Jul 05, 2021)</h1>
<h2>Features added</h2>
<ul>
<li>C, add C23 keywords <code>_Decimal32</code>, <code>_Decimal64</code>, and <code>_Decimal128</code>.</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9354">#9354</a>: C, add :confval:<code>c_extra_keywords</code> to allow user-defined keywords
during parsing.</li>
<li>Revert the removal of <code>sphinx.util:force_decode()</code> to become some 3rd party
extensions available again during 5.0</li>
</ul>
<h2>Bugs fixed</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9330">#9330</a>: changeset domain: :rst:dir:<code>versionchanged</code> with contents being a list
will cause error during pdf build</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9313">#9313</a>: LaTeX: complex table with merged cells broken since 4.0</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9305">#9305</a>: LaTeX: backslash may cause Improper discretionary list pdf build error
with Japanese engines</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9354">#9354</a>: C, remove special macro names from the keyword list.
See also :confval:<code>c_extra_keywords</code>.</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9322">#9322</a>: KeyError is raised on PropagateDescDomain transform</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>007795d</code></a> Bump to 4.0.3 final</li>
<li><a href=""><code>779d902</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9326">#9326</a> from tk0miya/rebirth_of_force_decode</li>
<li><a href=""><code>a1994ac</code></a> Merge branch '4.0.x' into rebirth_of_force_decode</li>
<li><a href=""><code>723ad78</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9334">#9334</a> from tk0miya/9322_KeyError_from_PropageteDescDomain</li>
<li><a href=""><code>072cdf2</code></a> Merge branch '4.0.x' into 9322_KeyError_from_PropageteDescDomain</li>
<li><a href=""><code>df5764d</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9356">#9356</a> from jakobandersen/c_extra_keywords</li>
<li><a href=""><code>50f5280</code></a> C, keyword changes</li>
<li><a href=""><code>8939a75</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9335">#9335</a> from jfbu/9305_platex_backslash_upquote</li>
<li><a href=""><code>ef9b55c</code></a> Fix <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9305">#9305</a> LaTeX: backslash in sphinxupquote error with Japanese</li>
<li><a href=""><code>7673cd6</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9333">#9333</a> from tk0miya/9330_versionchanged_breaks_list</li>
<li>Additional commits viewable in <a href="https://github.com/sphinx-doc/sphinx/compare/v4.0.2...v4.0.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sphinx&package-manager=pip&previous-version=4.0.2&new-version=4.0.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `71addbe1eb90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.