# Issue

**Title:** build(deps): bump actions/create-github-app-token from 3.2.0 to 3.3.0

## Description

Bumps [actions/create-github-app-token](https://github.com/actions/create-github-app-token) from 3.2.0 to 3.3.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/create-github-app-token/releases">actions/create-github-app-token's releases</a>.</em></p>
<blockquote>
<h2>v3.3.0</h2>
<h2><a href="https://github.com/actions/create-github-app-token/compare/v3.2.0...v3.3.0">3.3.0</a> (2026-10-12)</h2>
<h3>Features</h3>
<ul>
<li>update permission inputs (<a href="">#399</a>) (<a href="">a47236f</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li><strong>deps:</strong> bump nested undici from 6.24.0 to 6.29.0 (<a href="">#403</a>) (<a href="">12461a3</a>)</li>
<li><strong>deps:</strong> bump the production-dependencies group across 1 directory with 3 updates (<a href="">#395</a>) (<a href="">a69c19d</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/create-github-app-token/blob/main/CHANGELOG.md">actions/create-github-app-token's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<h2><a href="https://github.com/actions/create-github-app-token/compare/v3.2.0...v3.3.0">3.3.0</a> (2026-10-12)</h2>
<h3>Features</h3>
<ul>
<li>update permission inputs (<a href="">#399</a>) (<a href="">a47236f</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li><strong>deps:</strong> bump nested undici from 6.24.0 to 6.29.0 (<a href="">#403</a>) (<a href="">12461a3</a>)</li>
<li><strong>deps:</strong> bump the production-dependencies group across 1 directory with 3 updates (<a href="">#395</a>) (<a href="">a69c19d</a>)</li>
</ul>
<h2><a href="https://github.com/actions/create-github-app-token/compare/v3.1.1...v3.2.0">3.2.0</a> (2026-05-12)</h2>
<h3>Features</h3>
<ul>
<li>add support for enterprise-level GitHub Apps (<a href="">#263</a>) (<a href="">952a2a7</a>)</li>
<li>support full repository names in <code>repositories</code> input (<a href="">#372</a>) (<a href="">85eb8dd</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li><strong>deps:</strong> bump <code>@​actions/core</code> from 3.0.0 to 3.0.1 in the production-dependencies group (<a href="">#364</a>) (<a href="">43e5c34</a>)</li>
<li>validate private-key input (<a href="">#376</a>) (<a href="">f24bbd8</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>64ab729</code></a> chore(main): release 3.3.0 (<a href="">#402</a>)</li>
<li><a href=""><code>f3a828e</code></a> ci: create signed dist commits in release workflow (<a href="">#404</a>)</li>
<li><a href=""><code>655017f</code></a> docs: clarify when owner grants access to all repositories (<a href="">#378</a>)</li>
<li><a href=""><code>12461a3</code></a> fix(deps): bump nested undici from 6.24.0 to 6.29.0 (<a href="">#403</a>)</li>
<li><a href=""><code>a47236f</code></a> feat: update permission inputs (<a href="">#399</a>)</li>
<li><a href=""><code>a69c19d</code></a> fix(deps): bump the production-dependencies group across 1 directory with 3 u...</li>
<li><a href=""><code>d5cb7ae</code></a> build(deps): bump actions/checkout from 6 to 7 (<a href="">#384</a>)</li>
<li><a href=""><code>575da86</code></a> build(deps): bump stefanzweifel/git-auto-commit-action from 7.1.0 to 7.2.0 in...</li>
<li><a href=""><code>e85f677</code></a> test: omit stack traces from snapshots (<a href="">#401</a>)</li>
<li><a href=""><code>9419396</code></a> build(deps-dev): bump c8 from 11.0.0 to 12.0.0 (<a href="">#400</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/create-github-app-token/compare/bcd2ba49218906704ab6c1aa796996da409d3eb1...64ab729a6294000f5aa4a4bc0b73d1f32bc45510">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/create-github-app-token&package-manager=github_actions&previous-version=3.2.0&new-version=3.3.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f290036a8c58`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.