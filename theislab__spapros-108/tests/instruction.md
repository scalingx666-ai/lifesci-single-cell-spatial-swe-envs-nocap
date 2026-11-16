# Issue

**Title:** [DEPENDABOT]: Bump mypy from 0.812 to 0.902

## Description

Bumps [mypy](https://github.com/python/mypy) from 0.812 to 0.902.
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>defe53f</code></a> Bump version to 0.902</li>
<li><a href=""><code>5edeeab</code></a> Remove misleading list of default locations (<a href="https://github-redirect.dependabot.com/python/mypy/issues/10614">#10614</a>)</li>
<li><a href=""><code>12cf0bf</code></a> Don't suggest incompatible stub packages (<a href="https://github-redirect.dependabot.com/python/mypy/issues/10610">#10610</a>)</li>
<li><a href=""><code>8f51fbf</code></a> Fix confusion between stubs for google.protobuf and google.cloud (<a href="https://github-redirect.dependabot.com/python/mypy/issues/10609">#10609</a>)</li>
<li><a href=""><code>fee4e8c</code></a> Don't suggest installing types-pycrypto (<a href="https://github-redirect.dependabot.com/python/mypy/issues/10603">#10603</a>)</li>
<li><a href=""><code>ffc18df</code></a> Bump version to 0.901</li>
<li><a href=""><code>32d6b58</code></a> [mypyc] Fix evaluation of iterable in list comprehension twice</li>
<li><a href=""><code>b68993c</code></a> Bump version to 0.900</li>
<li><a href=""><code>be5aed7</code></a> Make ignore_missing_imports work for libs which had bundled stubs (<a href="https://github-redirect.dependabot.com/python/mypy/issues/10582">#10582</a>)</li>
<li><a href=""><code>e056774</code></a> Restrict the number of errors shown when there are missing stubs (<a href="https://github-redirect.dependabot.com/python/mypy/issues/10579">#10579</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/python/mypy/compare/v0.812...v0.902">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=mypy&package-manager=pip&previous-version=0.812&new-version=0.902)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac2cff57d0b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.