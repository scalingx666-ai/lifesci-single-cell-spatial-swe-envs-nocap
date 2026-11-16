# Issue

**Title:** build(deps): bump the actions-deps group with 3 updates

## Description

Bumps the actions-deps group with 3 updates: [docker/login-action](https://github.com/docker/login-action), [pypa/gh-action-pypi-publish](https://github.com/pypa/gh-action-pypi-publish) and [aws-actions/configure-aws-credentials](https://github.com/aws-actions/configure-aws-credentials).

Updates `docker/login-action` from 4.5.2 to 4.6.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/login-action/releases">docker/login-action's releases</a>.</em></p>
<blockquote>
<h2>v4.6.0</h2>
<ul>
<li>Harden buildx scoped config path handling by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#1059</a></li>
<li>Bump <code>@​aws-sdk/client-ecr</code> and <code>@​aws-sdk/client-ecr-public</code> to 3.1095.0 in <a href="">docker/login-action#1051</a></li>
<li>Bump js-yaml from 5.2.1 to 5.2.2 in <a href="">docker/login-action#1057</a></li>
<li>Bump postcss from 8.5.10 to 8.5.22 in <a href="">docker/login-action#1056</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v4.5.2...v4.6.0">https://github.com/docker/login-action/compare/v4.5.2...v4.6.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>dbcb813</code></a> Merge pull request <a href="">#1051</a> from docker/dependabot/npm_and_yarn/aws-sdk-dependen...</li>
<li><a href=""><code>5bcb015</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>b30b2f2</code></a> build(deps): bump the aws-sdk-dependencies group across 1 directory with 2 up...</li>
<li><a href=""><code>9087f1e</code></a> Merge pull request <a href="">#1057</a> from docker/dependabot/npm_and_yarn/js-yaml-5.2.2</li>
<li><a href=""><code>0009830</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>2325523</code></a> build(deps): bump js-yaml from 5.2.1 to 5.2.2</li>
<li><a href=""><code>4ec1d4a</code></a> Merge pull request <a href="">#1056</a> from docker/dependabot/npm_and_yarn/postcss-8.5.22</li>
<li><a href=""><code>5fc99ba</code></a> Merge pull request <a href="">#1053</a> from docker/dependabot/github_actions/aws-actions/co...</li>
<li><a href=""><code>e512bd5</code></a> Merge pull request <a href="">#1052</a> from docker/dependabot/github_actions/codeql-actions...</li>
<li><a href=""><code>a146c91</code></a> Merge pull request <a href="">#1059</a> from crazy-max/harden-buildx-scope-paths</li>
<li>Additional commits viewable in <a href="https://github.com/docker/login-action/compare/371161bbe7024a29a25c5e19bfcbc0804fe9ad2c...dbcb813823bdd20940b903addbd779551569679f">compare view</a></li>
</ul>
</details>
<br />

Updates `pypa/gh-action-pypi-publish` from 1.14.1 to 1.14.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pypa/gh-action-pypi-publish/releases">pypa/gh-action-pypi-publish's releases</a>.</em></p>
<blockquote>
<h2>v1.14.2</h2>
<!-- raw HTML omitted -->
<h2>🛠️ Urgh… Another release!? Again? Explain yourself!</h2>
<p>Looking at the diff, you'll only witness updates across the dependency tree. That's it! It's not a security fix or anything like that even, no. But you'll want this update.</p>
<blockquote>
<p>[!tip]
So what <em>most</em> people will find useful is <a href="https://github.com/takluyver"><code>@​takluyver</code></a><a href="https://github.com/sponsors/takluyver">💰</a>'s update of Twine to v7 that we use internally (<a href="">#416</a>). This version will let them upload their sdists and wheels containing core packaging metadata v2.5 to (Test)PyPI.</p>
</blockquote>
<h2>🧐 Tell me why..</h2>
<!-- raw HTML omitted -->
<!-- raw HTML omitted -->
<p>TL;DR non-pure-python projects with C-extensions tend to have dozens (sometimes hundreds) wheels to upload to PyPI per release. They are often quite big and take time to transfer over the network. People started noticing problems and coming up with DIY sharding workarounds like <a href="">aio-libs/aiohttp#13226</a> around July 23.
On this date, projects with a good amount of bytes to publish would start getting timeouts 5 minutes after the PyPI publishing job begun. The same job that worked just fine before.</p>
<p>I had to start pinging upstream library and ecosystem people, on GitHub and privately, to start making sense of what was happening. Eventually, we collectively concluded that GitHub must've shortened the lifetime of their OIDC identity — it seems to have used to be 10 minutes long (at some point in the past) and is now 5 minutes, apparently. It's not documented clearly, and we have not been able to get any clarity by attempting to contact GitHub through private channels, using personal connections.</p>
<p>Over the course of investigation, <a href="https://github.com/facutuesca"><code>@​facutuesca</code></a><a href="https://github.com/sponsors/facutuesca">💰</a> found and fixed a related underlying cache invalidation bug in <a href="">sigstore/sigstore-python#1838</a>, which he then coordinated propagation through the dependency chain updates in sigstore-python, pypi-attestations, gh-action-pypi-publish and gh-action-sigstore-python.</p>
<p>Mike's also discovered that Sigstore's Rekor slowdown seems to have become the main contributing cause of the last week's incident. He's collected some data to support this claim: <a href="https://publishing-five-minute-timeout.tiiny.site">https://publishing-five-minute-timeout.tiiny.site</a>.</p>
<!-- raw HTML omitted -->
<!-- raw HTML omitted -->
<h2>🫶 New Contributors</h2>
<ul>
<li><a href="https://github.com/davidbrochart"><code>@​davidbrochart</code></a> made their first contribution in <a href="">#415</a></li>
<li><a href="https://github.com/takluyver"><code>@​takluyver</code></a> made their first contribution in <a href="">#416</a></li>
</ul>
<p><strong>🪞 Full Diff</strong>: <a href="https://github.com/pypa/gh-action-pypi-publish/compare/v1.14.1...v1.14.2">https://github.com/pypa/gh-action-pypi-publish/compare/v1.14.1...v1.14.2</a></p>
<p><strong>🧔‍♂️ Release Manager:</strong> <a href="https://github.com/sponsors/webknjaz"><code>@​webknjaz</code></a> <a href="https://stand-with-ukraine.pp.ua">🇺🇦</a></p>
<p><strong>🙏 Special Thanks</strong> to <a href="https://github.com/davidbrochart"><code>@​davidbrochart</code></a><a href="https://github.com/sponsors/davidbrochart">💰</a> and <a href="https://github.com/Dreamsorcerer"><code>@​Dreamsorcerer</code></a><a href="https://github.com/sponsors/Dreamsorcerer">💰</a> for turning my attention (in <a href="">#415</a> and in private) to the newly surfaced corner case in GitHub's behavior that only affected a narrow category of projects while many others remained blissfully unaware. <a href="https://github.com/bdraco"><code>@​bdraco</code></a><a href="https://github.com/sponsors/bdraco">💰</a> came up with a DIY sharding workaround for aiohttp that served as a demo for other projects. <a href="https://github.com/miketheman"><code>@​miketheman</code></a><a href="https://github.com/sponsors/miketheman">💰</a> confirmed the Warehouse-side details. Also, <a href="https://github.com/jku"><code>@​jku</code></a><a href="https://github.com/sponsors/jku">💰</a> and <a href="https://github.com/woodruffw"><code>@​woodruffw</code></a><a href="https://github.com/sponsors/woodruffw">💰</a> helped work through, review and release the Sigstore ecosystem upstream libs.</p>
<p><strong>💬 Discuss</strong> <a href="https://bsky.app/profile/did:plc:ve6s3mxkefjaxty3m4fdqumn/post/3mrsqy2xba22j">on Bluesky 🦋</a>, <a href="https://mastodon.social/@webknjaz/117005132816750073">on Mastodon 🐘</a> and [on GitHub][release discussion].</p>
<p>[![GH Sponsors badge]][GH Sponsors URL]</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>dc37677</code></a> Merge pull request <a href="">#417</a> from trail-of-forks/ft/bump-deps</li>
<li><a href=""><code>8b2f234</code></a> Bump <code>pypi-attestations</code> and <code>sigstore</code></li>
<li><a href=""><code>78b72db</code></a> Merge pull request <a href="">#416</a> from takluyver/twine-v7</li>
<li><a href=""><code>92f4d2a</code></a> Update twine to v7</li>
<li>See full diff in <a href="https://github.com/pypa/gh-action-pypi-publish/compare/ba38be9e461d3875417946c167d0b5f3d385a247...dc37677b2e1c63e2034f94d8a5b11f265b73ba33">compare view</a></li>
</ul>
</details>
<br />

Updates `aws-actions/configure-aws-credentials` from 4.3.1 to 6.2.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/aws-actions/configure-aws-credentials/releases">aws-actions/configure-aws-credentials's releases</a>.</em></p>
<blockquote>
<h2>v6.2.3</h2>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.2.2...v6.2.3">6.2.3</a> (2026-07-22)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>attach git credentials before Tag Major Version push (<a href="">#1877</a>) (<a href="">9ae780b</a>)</li>
<li>PackedPolicyTooLarge detection in STS tags (<a href="">#1899</a>) (<a href="">fa8d6a5</a>)</li>
</ul>
<h2>v6.2.2</h2>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.2.1...v6.2.2">6.2.2</a> (2026-07-07)</h2>
<h3>Miscellaneous Chores</h3>
<ul>
<li>release 6.2.2 (<a href="">d01d678</a>)</li>
</ul>
<h2>v6.2.1</h2>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.2.0...v6.2.1">6.2.1</a> (2026-06-26)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>enforce allowed-account-ids on all auth paths (<a href="">#1847</a>) (<a href="">4d281fb</a>)</li>
</ul>
<h2>v6.2.0</h2>
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
<h2>v6.1.3</h2>
<h2><a href="https://github.com/aws-actions/configure-aws-credentials/compare/v6.1.2...v6.1.3">6.1.3</a> (2026-05-27)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>fix: allow kubelet token symlink in <a href="">aws-actions/configure-aws-credentials#1805</a></li>
</ul>
<h2>v6.1.2</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
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
<li><a href=""><code>e6de054</code></a> chore(main): release 6.2.3 (<a href="">#1878</a>)</li>
<li><a href=""><code>ab3b2ba</code></a> chore: Update dist</li>
<li><a href=""><code>fa8d6a5</code></a> fix: PackedPolicyTooLarge detection in STS tags (<a href="">#1899</a>)</li>
<li><a href=""><code>42e118a</code></a> chore(deps-dev): bump markdownlint-cli from 0.49.0 to 0.49.1 (<a href="">#1896</a>)</li>
<li><a href=""><code>d86ddfc</code></a> chore: Update dist</li>
<li><a href=""><code>874aaac</code></a> chore(deps): bump <code>@​aws-sdk/client-sts</code> from 3.1086.0 to 3.1091.0 (<a href="">#1892</a>)</li>
<li><a href=""><code>d4341b6</code></a> chore: Update dist</li>
<li><a href=""><code>fe51823</code></a> chore(deps-dev): bump <code>@​aws-sdk/credential-provider-env</code> (<a href="">#1894</a>)</li>
<li><a href=""><code>a8be382</code></a> chore(deps-dev): bump <code>@​biomejs/biome</code> from 2.5.3 to 2.5.4 (<a href="">#1893</a>)</li>
<li><a href=""><code>e000376</code></a> chore: Update dist</li>
<li>Additional commits viewable in <a href="https://github.com/aws-actions/configure-aws-credentials/compare/7474bc4690e29a8392af63c5b98e7449536d5c3a...e6de054238d6b7531b4efff3b6587d9aade6a06c">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0bedaa302c94`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.