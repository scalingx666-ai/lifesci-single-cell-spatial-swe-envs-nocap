# Issue

**Title:** build(deps): bump aws-actions/configure-aws-credentials from 6.2.3 to 6.2.4 in the actions-deps group

## Description

Bumps the actions-deps group with 1 update: [aws-actions/configure-aws-credentials](https://github.com/aws-actions/configure-aws-credentials).

Updates `aws-actions/configure-aws-credentials` from 6.2.3 to 6.2.4
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/aws-actions/configure-aws-credentials/releases">aws-actions/configure-aws-credentials's releases</a>.</em></p>
<blockquote>
<h2>v6.2.4</h2>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.2.3...v6.2.4">6.2.4</a> (2026-08-31)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>account-ids handling, mask proxy as secret in logs (<a href="">#1943</a>) (<a href="">aa65264</a>)</li>
<li>skip backoff sleep after the final retryAndBackoff attempt (<a href="">#1937</a>) (<a href="">3852440</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/aws-actions/configure-aws-credentials/blob/main/CHANGELOG.md">aws-actions/configure-aws-credentials's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<p>All notable changes to this project will be documented in this file. See <a href="https://github.com/conventional-changelog/standard-version">standard-version</a> for commit guidelines.</p>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.2.3...v6.2.4">6.2.4</a> (2026-08-31)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>account-ids handling, mask proxy as secret in logs (<a href="">#1943</a>) (<a href="">aa65264</a>)</li>
<li>skip backoff sleep after the final retryAndBackoff attempt (<a href="">#1937</a>) (<a href="">3852440</a>)</li>
</ul>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.2.2...v6.2.3">6.2.3</a> (2026-07-22)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>attach git credentials before Tag Major Version push (<a href="">#1877</a>) (<a href="">9ae780b</a>)</li>
<li>PackedPolicyTooLarge detection in STS tags (<a href="">#1899</a>) (<a href="">fa8d6a5</a>)</li>
</ul>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.2.1...v6.2.2">6.2.2</a> (2026-07-07)</h2>
<h3>Miscellaneous Chores</h3>
<ul>
<li>release 6.2.2 (<a href="">d01d678</a>)</li>
</ul>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.2.0...v6.2.1">6.2.1</a> (2026-06-26)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>enforce allowed-account-ids on all auth paths (<a href="">#1847</a>) (<a href="">4d281fb</a>)</li>
</ul>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.1.3...v6.2.0">6.2.0</a> (2026-06-01)</h2>
<h3>Features</h3>
<ul>
<li>add additional session tags by default (<a href="">#1775</a>) (<a href="">e0ba768</a>)</li>
<li>add more retry logic and better logging (<a href="">#1764</a>) (<a href="">540d0c1</a>)</li>
<li>add regex validation to role-session-name (<a href="">#1765</a>) (<a href="">e354499</a>)</li>
<li>Allow custom session tags to be passed when assuming a role (<a href="">#1759</a>) (<a href="">61f50f6</a>)</li>
<li>expose run id in STS client user-agent (<a href="">#1774</a>) (<a href="">29d1be3</a>)</li>
<li>support custom STS endpoints (<a href="">#1762</a>) (<a href="">8d52d05</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>skip credential check on output-env-credentials: false (<a href="">#1778</a>) (<a href="">58e7c47</a>)</li>
<li>assumeRole failing from session tag size too large (<a href="">#1808</a>) (<a href="">d6f5dc3</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cbe3b39</code></a> chore(main): release 6.2.4 (<a href="">#1942</a>)</li>
<li><a href=""><code>58065db</code></a> chore(deps): bump js-yaml (<a href="">#1944</a>)</li>
<li><a href=""><code>609df23</code></a> chore: Update dist</li>
<li><a href=""><code>aa65264</code></a> fix: account-ids handling, mask proxy as secret in logs (<a href="">#1943</a>)</li>
<li><a href=""><code>7fdbbb8</code></a> chore: Update dist</li>
<li><a href=""><code>3852440</code></a> fix: skip backoff sleep after the final retryAndBackoff attempt (<a href="">#1937</a>)</li>
<li><a href=""><code>c16f89b</code></a> mention renamed repos use the new immutable identifiers (<a href="">#1941</a>)</li>
<li><a href=""><code>9c362ee</code></a> chore: Update dist</li>
<li><a href=""><code>d5f8da8</code></a> chore(deps): bump <code>@​aws-sdk/client-sts</code> from 3.1111.0 to 3.1116.0 (<a href="">#1935</a>)</li>
<li><a href=""><code>2db2497</code></a> chore: Update dist</li>
<li>Additional commits viewable in <a href="https://github.com/aws-actions/configure-aws-credentials/compare/e6de054238d6b7531b4efff3b6587d9aade6a06c...cbe3b392738ccf3f987d68400dafcf4b0624a56c">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=aws-actions/configure-aws-credentials&package-manager=github_actions&previous-version=6.2.3&new-version=6.2.4)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa8499c69733`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.