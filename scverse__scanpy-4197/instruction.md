# Issue

**Title:** ci: bump astral-sh/setup-uv from 8.2.0 to 8.3.0

## Description

Bumps [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv) from 8.2.0 to 8.3.0.
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d31148d</code></a> Strip environment markers from detected uv dependency pins (<a href="">#938</a>)</li>
<li><a href=""><code>17c3989</code></a> Fix cache keys for Python version ranges (<a href="">#937</a>)</li>
<li><a href=""><code>3cc3c11</code></a> chore(deps): roll up Dependabot updates (<a href="">#936</a>)</li>
<li><a href=""><code>9225f84</code></a> chore(deps): bump release-drafter/release-drafter from 7.3.1 to 7.4.0 (<a href="">#924</a>)</li>
<li><a href=""><code>fc16fa3</code></a> chore(deps): bump actions/checkout from 6.0.2 to 7.0.0 (<a href="">#926</a>)</li>
<li><a href=""><code>a1a7345</code></a> ci: call docs update workflow from release (<a href="">#933</a>)</li>
<li><a href=""><code>a5e9cbf</code></a> docs: update version references to v8.2.0 (<a href="">#932</a>)</li>
<li><a href=""><code>c5680ec</code></a> chore: update known checksums for 0.11.26 (<a href="">#930</a>)</li>
<li><a href=""><code>c86fe4e</code></a> Add a threat model for setup-uv (<a href="">#923</a>)</li>
<li><a href=""><code>224c887</code></a> chore: update known checksums for 0.11.25 (<a href="">#929</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/setup-uv/compare/v8.2.0...v8.3.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=astral-sh/setup-uv&package-manager=github_actions&previous-version=8.2.0&new-version=8.3.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `537e42022d6f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.