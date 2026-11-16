# Issue

**Title:** Bump human-panic from 1.0.1 to 1.1.5

## Description

Bumps [human-panic](https://github.com/rust-cli/human-panic) from 1.0.1 to 1.1.5.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-cli/human-panic/blob/master/CHANGELOG.md">human-panic's changelog</a>.</em></p>
<blockquote>
<h2>[1.1.5] - 2023-06-13</h2>
<h3>Fixes</h3>
<ul>
<li>Avoid symbol conflicts from macros</li>
</ul>
<h2>[1.1.4] - 2023-04-13</h2>
<h3>Internal</h3>
<ul>
<li>Dependency update</li>
</ul>
<h2>[1.1.3] - 2023-03-16</h2>
<h3>Internal</h3>
<ul>
<li>Dependency update</li>
</ul>
<h2>[1.1.2] - 2023-03-14</h2>
<h3>Compatibility</h3>
<ul>
<li>Update MSRV to 1.64.0</li>
</ul>
<h3>Fixes</h3>
<ul>
<li>Correctly handle <code>CLICOLOR=1</code></li>
<li>Correctly handle <code>NO_COLOR=</code></li>
<li>Auto-enable color for CI</li>
<li>Update a macro to use <code>$crate</code></li>
</ul>
<h2>[1.1.1] - 2023-02-28</h2>
<h3>Internal</h3>
<ul>
<li>Update dependencies</li>
</ul>
<h2>[1.1.0] - 2023-02-01</h2>
<h3>Features</h3>
<ul>
<li>Expose <code>metadata!</code> constructor</li>
<li>Expose <code>PanicStyle::default()</code> for knowing which handler to use::</li>
</ul>
<h3>Fixes</h3>
<ul>
<li>Detect when color can be used</li>
<li>Make color optional (opt-out)</li>
</ul>
<h2>[v1.0.3]</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>69ac491</code></a> chore: Release</li>
<li><a href=""><code>be6837a</code></a> docs: Update changelog</li>
<li><a href=""><code>432726b</code></a> chore: Fix spelling</li>
<li><a href=""><code>edc6d92</code></a> Merge pull request <a href="">#109</a> from dead-claudia/patch-1</li>
<li><a href=""><code>7b13ad7</code></a> Ensure macro-internal variables are properly encapsulated</li>
<li><a href=""><code>acdfb96</code></a> Merge pull request <a href="">#108</a> from matthiasbeyer/explain-where-macro</li>
<li><a href=""><code>dff2180</code></a> Explain where setup_panic!() should be called</li>
<li><a href=""><code>35b1a08</code></a> chore: Update owners</li>
<li><a href=""><code>eb3d341</code></a> chore: Add rust-cli as owners</li>
<li><a href=""><code>637c6dc</code></a> chore(ci): Fix default branch</li>
<li>Additional commits viewable in <a href="https://github.com/rust-cli/human-panic/compare/1.0.1...v1.1.5">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=human-panic&package-manager=cargo&previous-version=1.0.1&new-version=1.1.5)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ec9a4a00017`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.