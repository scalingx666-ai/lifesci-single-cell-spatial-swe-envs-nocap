# Issue

**Title:** build(deps): bump the actions-deps group with 2 updates

## Description

Bumps the actions-deps group with 2 updates: [docker/login-action](https://github.com/docker/login-action) and [aws-actions/configure-aws-credentials](https://github.com/aws-actions/configure-aws-credentials).

Updates `docker/login-action` from 4.5.1 to 4.5.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/login-action/releases">docker/login-action's releases</a>.</em></p>
<blockquote>
<h2>v4.5.2</h2>
<ul>
<li>Surface Docker Hub OIDC error responses by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#1058</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v4.5.1...v4.5.2">https://github.com/docker/login-action/compare/v4.5.1...v4.5.2</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>371161b</code></a> Merge pull request <a href="">#1058</a> from crazy-max/fix-dockerhub-oidc-error-handling</li>
<li><a href=""><code>5dc73df</code></a> chore: update generated content</li>
<li><a href=""><code>2aa1ede</code></a> surface Docker Hub OIDC error responses</li>
<li>See full diff in <a href="https://github.com/docker/login-action/compare/abd2ef45e78c5afb21d64d4ca52ee8550d9572c7...371161bbe7024a29a25c5e19bfcbc0804fe9ad2c">compare view</a></li>
</ul>
</details>
<br />

Updates `aws-actions/configure-aws-credentials` from ff717079ee2060e4bcee96c4779b553acc87447c to 7474bc4690e29a8392af63c5b98e7449536d5c3a
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/aws-actions/configure-aws-credentials/blob/main/CHANGELOG.md">aws-actions/configure-aws-credentials's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<p>All notable changes to this project will be documented in this file. See <a href="https://github.com/conventional-changelog/standard-version">standard-version</a> for commit guidelines.</p>
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
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.1.2...v6.1.3">6.1.3</a> (2026-05-28)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>fix: allow kubelet token symlink in <a href="">#1805</a></li>
</ul>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.1.1...v6.1.2">6.1.2</a> (2026-05-26)</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/aws-actions/configure-aws-credentials/compare/ff717079ee2060e4bcee96c4779b553acc87447c...7474bc4690e29a8392af63c5b98e7449536d5c3a">compare view</a></li>
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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4e587cc2e07`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.