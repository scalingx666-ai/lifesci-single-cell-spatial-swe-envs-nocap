# Issue

**Title:** [DEPENDABOT]: Bump sphinx from 3.5.1 to 3.5.2

## Description

Bumps [sphinx](https://github.com/sphinx-doc/sphinx) from 3.5.1 to 3.5.2.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/blob/3.x/CHANGES">sphinx's changelog</a>.</em></p>
<blockquote>
<h1>Release 3.5.2 (released Mar 06, 2021)</h1>
<h2>Bugs fixed</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8943">#8943</a>: i18n: Crashed by broken translation messages in ES, EL and HR</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8936">#8936</a>: LaTeX: A custom LaTeX builder fails with unknown node error</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8952">#8952</a>: Exceptions raised in a Directive cause parallel builds to hang</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a969e90</code></a> Bump to 3.5.2 final</li>
<li><a href=""><code>a6158b4</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8956">#8956</a> from tk0miya/8943_update_translations</li>
<li><a href=""><code>3cd1030</code></a> Merge branch '3.5.x' into 8943_update_translations</li>
<li><a href=""><code>cb14587</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8958">#8958</a> from tk0miya/8936_custom_latex_builder</li>
<li><a href=""><code>866e244</code></a> Merge branch '3.5.x' into 8936_custom_latex_builder</li>
<li><a href=""><code>ad10c62</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8957">#8957</a> from tk0miya/8952_hangup_on_parallel_build</li>
<li><a href=""><code>f75e86d</code></a> Fix <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8936">#8936</a>: LaTeX: A custom LaTeX builder fails with unknown node error</li>
<li><a href=""><code>ec6ab72</code></a> Fix <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8952">#8952</a>: Exceptions raised in a Directive cause parallel builds to hang</li>
<li><a href=""><code>bae8fb6</code></a> i18n: Fix wrong substitution message catalog for el and hr (refs: <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8943">#8943</a>)</li>
<li><a href=""><code>99d97c6</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8943">#8943</a> from askhl/3.5.x-fix-spanish-template</li>
<li>Additional commits viewable in <a href="https://github.com/sphinx-doc/sphinx/compare/v3.5.1...v3.5.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sphinx&package-manager=pip&previous-version=3.5.1&new-version=3.5.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f82ee41906ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.