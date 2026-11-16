# Issue

**Title:** [DEPENDABOT]: Bump pygments from 2.8.0 to 2.8.1

## Description

[//]: # (dependabot-start)
⚠️  **Dependabot is rebasing this PR** ⚠️

If you make any changes to it yourself then they will take precedence over the rebase.

---

[//]: # (dependabot-end)

Bumps [pygments](https://github.com/pygments/pygments) from 2.8.0 to 2.8.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pygments/pygments/releases">pygments's releases</a>.</em></p>
<blockquote>
<h2>2.8.1</h2>
<ul>
<li>Fix issue with LaTeX formatter and <code>minted</code> (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1734">#1734</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1735">#1735</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1736">#1736</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1737">#1737</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pygments/pygments/blob/2.8.1/CHANGES">pygments's changelog</a>.</em></p>
<blockquote>
<h2>Version 2.8.1</h2>
<p>(released March 7, 2021)</p>
<ul>
<li>Fix issue with LaTeX formatter and <code>minted</code> (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1734">#1734</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1735">#1735</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1736">#1736</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1737">#1737</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d356f2e</code></a> Prepare 2.8.1 release.</li>
<li><a href=""><code>c462a2a</code></a> Update CHANGES.</li>
<li><a href=""><code>0fe8b03</code></a> Update CHANGES.</li>
<li><a href=""><code>df8ae3c</code></a> Minted compatibility patch (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1737">#1737</a>)</li>
<li><a href=""><code>48f58c9</code></a> Update CHANGES.</li>
<li><a href=""><code>500713d</code></a> LaTeX: workaround minted incompatibility with Pygments 2.8.0 (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1735">#1735</a>)</li>
<li>See full diff in <a href="https://github.com/pygments/pygments/compare/2.8.0...2.8.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pygments&package-manager=pip&previous-version=2.8.0&new-version=2.8.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8337573cadc1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.