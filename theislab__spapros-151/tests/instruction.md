# Issue

**Title:** [DEPENDABOT]: Bump sphinx from 4.1.1 to 4.1.2

## Description

Bumps [sphinx](https://github.com/sphinx-doc/sphinx) from 4.1.1 to 4.1.2.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/blob/4.x/CHANGES">sphinx's changelog</a>.</em></p>
<blockquote>
<h1>Release 4.1.2 (released Jul 27, 2021)</h1>
<h2>Incompatible changes</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9435">#9435</a>: linkcheck: Disable checking automatically generated anchors on
github.com (ex. anchors in reST/Markdown documents)</li>
</ul>
<h2>Bugs fixed</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9489">#9489</a>: autodoc: Custom types using <code>typing.NewType</code> are not displayed well
with the HEAD of 3.10</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9490">#9490</a>: autodoc: Some objects under <code>typing</code> module are not displayed well
with the HEAD of 3.10</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9436">#9436</a>, <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9471">#9471</a>: autodoc: crashed if <code>autodoc_class_signature = &quot;separated&quot;</code></li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9456">#9456</a>: html search: html_copy_source can't control the search summaries</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9435">#9435</a>: linkcheck: Failed to check anchors in github.com</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4ba5c21</code></a> Bump to 4.1.2 final</li>
<li><a href=""><code>4dc45f0</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9494">#9494</a> from tk0miya/9456_revert_9129</li>
<li><a href=""><code>df562b4</code></a> Merge branch '4.1.x' into 9456_revert_9129</li>
<li><a href=""><code>5d8f925</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9493">#9493</a> from tk0miya/9436_autodoc_class_signature</li>
<li><a href=""><code>ef53dec</code></a> Fix <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9456">#9456</a>: html search: html_copy_source can't control the search summaries</li>
<li><a href=""><code>4f364a3</code></a> Fix <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9436">#9436</a>, <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9471">#9471</a>: autodoc: crashed if autodoc_class_signature = &quot;separated&quot;</li>
<li><a href=""><code>9218ad4</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9491">#9491</a> from tk0miya/9489_NewType</li>
<li><a href=""><code>68fb548</code></a> Fix <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9490">#9490</a>: autodoc: Some typing.* objects are broken</li>
<li><a href=""><code>771507e</code></a> Fix <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9489">#9489</a>: autodoc: Custom types using typing.NewType are broken</li>
<li><a href=""><code>9ebdc98</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9467">#9467</a> from tk0miya/9435_disable_rewrite_github_anchor</li>
<li>Additional commits viewable in <a href="https://github.com/sphinx-doc/sphinx/compare/v4.1.1...v4.1.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sphinx&package-manager=pip&previous-version=4.1.1&new-version=4.1.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac912c5ddefd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.