# Issue

**Title:** [DEPENDABOT]: Bump flake8-bugbear from 21.3.1 to 21.3.2

## Description

Bumps [flake8-bugbear](https://github.com/PyCQA/flake8-bugbear) from 21.3.1 to 21.3.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/PyCQA/flake8-bugbear/releases">flake8-bugbear's releases</a>.</em></p>
<blockquote>
<h2>2020.11.1</h2>
<ul>
<li>Support exception aliases properly in B014 (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/129">#129</a>)</li>
<li>Add B015: Pointless comparison (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/130">#130</a>)</li>
<li>Remove check for # noqa comments (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/134">#134</a>)</li>
<li>Ignore exception classes which are not types (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/135">#135</a>)</li>
<li>Introduce B016 to check for raising a literal. (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/141">#141</a>)</li>
<li>Exclude types.MappingProxyType() from B008. (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/144">#144</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/PyCQA/flake8-bugbear/commits">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=flake8-bugbear&package-manager=pip&previous-version=21.3.1&new-version=21.3.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9e84e6c7acf2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.