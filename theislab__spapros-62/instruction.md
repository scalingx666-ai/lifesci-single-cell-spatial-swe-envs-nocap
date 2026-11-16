# Issue

**Title:** [DEPENDABOT]: Bump actions/cache from v2.1.4 to v2.1.5

## Description

Bumps [actions/cache](https://github.com/actions/cache) from v2.1.4 to v2.1.5.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/cache/releases">actions/cache's releases</a>.</em></p>
<blockquote>
<h2>v2.1.5</h2>
<ul>
<li>Fix permissions error seen when extracting caches with GNU tar that were previously created using BSD tar (<a href="https://github-redirect.dependabot.com/actions/cache/issues/527">actions/cache#527</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1a9e213</code></a> Update cache module to v1.0.7 (<a href="https://github-redirect.dependabot.com/actions/cache/issues/562">#562</a>)</li>
<li><a href=""><code>981fa98</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/cache/issues/469">#469</a> from ericmj/patch-1</li>
<li><a href=""><code>4498c5b</code></a> Drop the example based on using pip's internals (<a href="https://github-redirect.dependabot.com/actions/cache/issues/519">#519</a>)</li>
<li><a href=""><code>4134e6d</code></a> It is not recommended to cache node_modules (<a href="https://github-redirect.dependabot.com/actions/cache/issues/537">#537</a>)</li>
<li><a href=""><code>62a4d75</code></a> Also cache _build for Elixir</li>
<li>See full diff in <a href="https://github.com/actions/cache/compare/v2.1.4...1a9e2138d905efd099035b49d8b7a3888c653ca8">compare view</a></li>
</ul>
</details>
<br />

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d78c787dcb7e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.