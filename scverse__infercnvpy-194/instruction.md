# Issue

**Title:** Bump the actions-deps group with 2 updates

## Description

Bumps the actions-deps group with 2 updates: [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv) and [pypa/gh-action-pypi-publish](https://github.com/pypa/gh-action-pypi-publish).

Updates `astral-sh/setup-uv` from 10.1.0 to 10.3.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/setup-uv/releases">astral-sh/setup-uv's releases</a>.</em></p>
<blockquote>
<h2>v10.3.3 🌈 Use Astral mirror for version manifests with GitHub fallback</h2>
<h2>Changes</h2>
<p>This release contains something that should have been included a very long time ago. Sorry for sleeping on that.</p>
<p>This action now retrieves the release manifest that contains the available versions, their download links and checksums from the Astral mirror, rather than trying GitHub first. This should present much more stable.
(Known checksums are still checked, so the security impact does not change)</p>
<p>Also a big thank you to <a href="https://github.com/soujasK"><code>@​soujasK</code></a> for a set of bugfixes 👏</p>
<h2>🐛 Bug fixes</h2>
<ul>
<li>Use Astral mirror for version manifests with GitHub fallback <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#1119</a>)</li>
<li>fix: allow whitespace in uv requirement specifiers <a href="https://github.com/soujasK"><code>@​soujasK</code></a> (<a href="">#1112</a>)</li>
<li>fix: resolve ~= specifiers with PEP 440 semantics <a href="https://github.com/soujasK"><code>@​soujasK</code></a> (<a href="">#1111</a>)</li>
<li>fix: only report a saved cache when saving succeeded <a href="https://github.com/soujasK"><code>@​soujasK</code></a> (<a href="">#1110</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.13.6 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1117</a>)</li>
</ul>
<h2>📚 Documentation</h2>
<ul>
<li>docs: use JSDoc for compatible release specifier comment <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#1113</a>)</li>
<li>docs: update version references to v10.3.2 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1104</a>)</li>
</ul>
<h2>v10.3.2 🌈 update known checksums for 0.13.5</h2>
<h2>Changes</h2>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.13.5 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1103</a>)</li>
</ul>
<h2>📚 Documentation</h2>
<ul>
<li>docs: update version references to v10.3.1 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1102</a>)</li>
</ul>
<h2>v10.3.1 🌈 preserve cache error class names in save-cache bundle</h2>
<h2>Changes</h2>
<p>This release includes a fix so that multiple concurrent workflows trying to upload the same cache no longer warn</p>
<p><code>##[warning]Failed to save: Unable to reserve cache with key ..., another job may be creating this cache.</code></p>
<h2>🐛 Bug fixes</h2>
<ul>
<li>fix: preserve cache error class names in save-cache bundle <a href="https://github.com/dannyward630"><code>@​dannyward630</code></a> (<a href="">#1093</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>68559e9</code></a> Use Astral mirror for version manifests with GitHub fallback (<a href="">#1119</a>)</li>
<li><a href=""><code>0192b69</code></a> chore: update known checksums for 0.13.6 (<a href="">#1117</a>)</li>
<li><a href=""><code>2f29784</code></a> docs: use JSDoc for compatible release specifier comment (<a href="">#1113</a>)</li>
<li><a href=""><code>9c73321</code></a> fix: allow whitespace in uv requirement specifiers (<a href="">#1112</a>)</li>
<li><a href=""><code>80fbe01</code></a> fix: resolve ~= specifiers with PEP 440 semantics (<a href="">#1111</a>)</li>
<li><a href=""><code>36b7b57</code></a> fix: only report a saved cache when saving succeeded (<a href="">#1110</a>)</li>
<li><a href=""><code>56618ca</code></a> docs: update version references to v10.3.2 (<a href="">#1104</a>)</li>
<li><a href=""><code>07a047e</code></a> chore: update known checksums for 0.13.5 (<a href="">#1103</a>)</li>
<li><a href=""><code>e1b8536</code></a> docs: update version references to v10.3.1 (<a href="">#1102</a>)</li>
<li><a href=""><code>18d369b</code></a> chore(deps): roll up Dependabot updates (<a href="">#1101</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/setup-uv/compare/bec219d24cd3e171d82865faccec33120bb574f4...68559e99cc807c1eb7e9238fd43a15bba460eec2">compare view</a></li>
</ul>
</details>
<br />

Updates `pypa/gh-action-pypi-publish` from 1.14.2 to 1.14.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pypa/gh-action-pypi-publish/releases">pypa/gh-action-pypi-publish's releases</a>.</em></p>
<blockquote>
<h2>v1.14.3</h2>
<!-- raw HTML omitted -->
<blockquote>
<p>[!important]
🚨 This release includes fixes for <a href="https://github.com/pypa/gh-action-pypi-publish/security/advisories/GHSA-5xjx-3w67-w9x9">GHSA-5xjx-3w67-w9x9</a> patched up by <a href="https://github.com/sethmlarson"><code>@​sethmlarson</code></a><a href="https://github.com/sponsors/sethmlarson">💰</a> in <a href="">#427</a> and in other places across the ecosystem.</p>
<p>Additional ecosystem and related mitigations beyond you might want to watch out for:</p>
<ul>
<li><a href="https://discuss.python.org/t/information-for-python-users-regarding-emudhra-emsign-ca-certificate-security-incident/109576">https://discuss.python.org/t/information-for-python-users-regarding-emudhra-emsign-ca-certificate-security-incident/109576</a></li>
<li><a href="https://emudhra.we-have-a-problem.com">https://emudhra.we-have-a-problem.com</a></li>
</ul>
</blockquote>
<h2>🛠️ Security Tightening</h2>
<p><a href="https://github.com/webknjaz"><code>@​webknjaz</code></a><a href="https://github.com/sponsors/webknjaz">💰</a> made sure the dependency tree within the action runtime uses hash-checking from now on via <a href="">pypa/gh-action-pypi-publish#420</a>.</p>
<p><strong>🪞 Full Diff</strong>: <a href="https://github.com/pypa/gh-action-pypi-publish/compare/v1.14.2...v1.14.3">https://github.com/pypa/gh-action-pypi-publish/compare/v1.14.2...v1.14.3</a></p>
<p><strong>🧔‍♂️ Release Manager:</strong> <a href="https://github.com/sponsors/webknjaz"><code>@​webknjaz</code></a> <a href="https://stand-with-ukraine.pp.ua">🇺🇦</a></p>
<p><strong>💬 Discuss</strong> <a href="https://bsky.app/profile/webknjaz.me/post/3mydcjweyak2f">on Bluesky 🦋</a>, <a href="https://mastodon.social/@webknjaz/117474743338290807">on Mastodon 🐘</a> and <a href="https://github.com/pypa/gh-action-pypi-publish/discussions/429">on GitHub</a>.</p>
<p><a href="https://github.com/sponsors/webknjaz"><img src="https://img.shields.io/badge/%40webknjaz-transparent?logo=githubsponsors&amp;logoColor=%23EA4AAA&amp;label=Sponsor&amp;color=2a313c" alt="GH Sponsors badge" /></a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7245906</code></a> Merge pull request <a href="">#427</a> from sethmlarson/certifi-sigstore</li>
<li><a href=""><code>331eccb</code></a> Upgrade certifi and sigstore</li>
<li><a href=""><code>f68fee4</code></a> 💰 Sync the FUNDING config</li>
<li><a href=""><code>c0d6f8e</code></a> Merge branch 'integrity/runtime/deptree' into unstable/v1</li>
<li><a href=""><code>9090099</code></a> 🧪 Make smoke test deps hash-pinned in CI</li>
<li><a href=""><code>34e40c2</code></a> 📌 Bump pip-tools managed transitive deptrees</li>
<li><a href=""><code>e800ed5</code></a> 👷 Enable hash-checking in the runtime deptree 🔗</li>
<li><a href=""><code>dd8c5f4</code></a> 🔧 Make pip-tools config available in container</li>
<li>See full diff in <a href="https://github.com/pypa/gh-action-pypi-publish/compare/dc37677b2e1c63e2034f94d8a5b11f265b73ba33...7245906fb61fa33a13554f9d5fb856fe61758086">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18a08639367e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.