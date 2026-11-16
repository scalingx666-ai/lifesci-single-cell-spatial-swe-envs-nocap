# Issue

**Title:** Bump actions/checkout from 5.0.1 to 5.1.0

## Description

Bumps [actions/checkout](https://github.com/actions/checkout) from 5.0.1 to 5.1.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/releases">actions/checkout's releases</a>.</em></p>
<blockquote>
<h2>v5.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li><strong>[BREAKING]</strong> backport <code>allow-unsafe-pr-checkout</code> to v5 by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2501</a></li>
<li>backport fixes to releases-v5 by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2523</a></li>
</ul>
<p><a href="https://github.blog/changelog/2026-06-18-safer-pull_request_target-defaults-for-github-actions-checkout/">https://github.blog/changelog/2026-06-18-safer-pull_request_target-defaults-for-github-actions-checkout/</a> for more details about this breaking change</p>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v5.0.1...v5.1.0">https://github.com/actions/checkout/compare/v5.0.1...v5.1.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>fbc6f39</code></a> backport fixes to releases-v5 (<a href="">#2523</a>)</li>
<li><a href=""><code>6026fb2</code></a> backport <code>allow-unsafe-pr-checkout</code> to v5 (<a href="">#2501</a>)</li>
<li>See full diff in <a href="https://github.com/actions/checkout/compare/93cb6efe18208431cddfb8368fd83d5badbf9bfd...fbc6f3992d24b796d5a048ff273f7fcc4a7b6c09">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/checkout&package-manager=github_actions&previous-version=5.0.1&new-version=5.1.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5bb59f567c4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.