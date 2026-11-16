# Issue

**Title:** Bump the actions-deps group across 1 directory with 4 updates

## Description

Bumps the actions-deps group with 4 updates in the / directory: [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv), [conda-incubator/setup-miniconda](https://github.com/conda-incubator/setup-miniconda), [pypa/gh-action-pypi-publish](https://github.com/pypa/gh-action-pypi-publish) and [codecov/codecov-action](https://github.com/codecov/codecov-action).

Updates `astral-sh/setup-uv` from 10.0.1 to 10.3.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/setup-uv/releases">astral-sh/setup-uv's releases</a>.</em></p>
<blockquote>
<h2>v10.3.1 🌈 preserve cache error class names in save-cache bundle</h2>
<h2>Changes</h2>
<p>This release includes a fix so that multiple concurrent workflows trying to upload the same cache no longer warn</p>
<p><code>##[warning]Failed to save: Unable to reserve cache with key ..., another job may be creating this cache.</code></p>
<h2>🐛 Bug fixes</h2>
<ul>
<li>fix: preserve cache error class names in save-cache bundle <a href="https://github.com/dannyward630"><code>@​dannyward630</code></a> (<a href="">#1093</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.13.4 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1099</a>)</li>
<li>chore: update known checksums for 0.13.2/0.13.3 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1098</a>)</li>
<li>chore: update known checksums for 0.13.1 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1094</a>)</li>
<li>Verify npm dependency signatures before builds <a href="https://github.com/zaniebot"><code>@​zaniebot</code></a> (<a href="">#1027</a>)</li>
</ul>
<h2>📚 Documentation</h2>
<ul>
<li>docs: cache-dependency-glob matches relative to the working directory <a href="https://github.com/flange-ipb"><code>@​flange-ipb</code></a> (<a href="">#1092</a>)</li>
<li>docs: update version references to v10.3.0 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1090</a>)</li>
</ul>
<h2>⬆️ Dependency updates</h2>
<ul>
<li>chore(deps): roll up Dependabot updates <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#1101</a>)</li>
</ul>
<h2>v10.3.0 🌈 Add Python architecture selection</h2>
<h2>Changes</h2>
<p>This release adds the <code>python-arch</code> input to select a Python architecture independently of the Python version. With <code>uv</code> 0.13.0 or later, set <code>python-arch: x86_64</code> to use x64 Python on Windows ARM64 runners.</p>
<p>It also includes embedded checksums for <code>uv</code> releases through 0.13.0.</p>
<ul>
<li>Use macOS 15 runners for tests <a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a> (<a href="">#1081</a>)</li>
</ul>
<h2>🚀 Enhancements</h2>
<ul>
<li>Add <code>python-arch</code> support <a href="https://github.com/zanieb"><code>@​zanieb</code></a> (<a href="">#1079</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.13.0 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1089</a>)</li>
<li>chore: update known checksums for 0.12.24 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1084</a>)</li>
<li>chore: update known checksums for 0.12.23 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1082</a>)</li>
<li>chore: update known checksums for 0.12.22 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1080</a>)</li>
<li>chore: update known checksums for 0.12.21 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1078</a>)</li>
<li>chore: update known checksums for 0.12.20 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1076</a>)</li>
<li>chore: update known checksums for 0.12.19 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1068</a>)</li>
<li>chore: update known checksums for 0.12.18 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1065</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>18d369b</code></a> chore(deps): roll up Dependabot updates (<a href="">#1101</a>)</li>
<li><a href=""><code>4ad2329</code></a> chore: update known checksums for 0.13.4 (<a href="">#1099</a>)</li>
<li><a href=""><code>4bc6759</code></a> chore: update known checksums for 0.13.2/0.13.3 (<a href="">#1098</a>)</li>
<li><a href=""><code>c97f06e</code></a> fix: preserve cache error class names in save-cache bundle (<a href="">#1093</a>)</li>
<li><a href=""><code>8ca4be0</code></a> chore: update known checksums for 0.13.1 (<a href="">#1094</a>)</li>
<li><a href=""><code>b627d85</code></a> docs: cache-dependency-glob matches relative to the working directory (<a href="">#1092</a>)</li>
<li><a href=""><code>f8c8897</code></a> Verify npm dependency signatures before builds (<a href="">#1027</a>)</li>
<li><a href=""><code>f64d32b</code></a> docs: update version references to v10.3.0 (<a href="">#1090</a>)</li>
<li><a href=""><code>1c37ad0</code></a> chore: update known checksums for 0.13.0 (<a href="">#1089</a>)</li>
<li><a href=""><code>b3c9b5f</code></a> chore: update known checksums for 0.12.24 (<a href="">#1084</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/setup-uv/compare/20cfd1bf945f4377ade1205e4dbc17946fc9a30d...18d369b23da25a81e9458561248e1aafff6a70fa">compare view</a></li>
</ul>
</details>
<br />

Updates `conda-incubator/setup-miniconda` from 4.0.1 to 4.1.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/conda-incubator/setup-miniconda/releases">conda-incubator/setup-miniconda's releases</a>.</em></p>
<blockquote>
<h2>Version 4.1.0</h2>
<h2>What's Changed</h2>
<h3>Features and Enhancements</h3>
<ul>
<li><a href="">#567</a>[567]: Add Miniforge support for <code>linux-riscv64</code></li>
</ul>
<h3>Fixes</h3>
<ul>
<li><a href="">#539</a><a href="">539</a>: Look up the tool cache by tool name to fix Miniconda3 cache
misses</li>
</ul>
<h3>Tasks and Maintenance</h3>
<ul>
<li><a href="">#507</a><a href="">507</a>: Harden GitHub Actions workflows and add zizmor scanning</li>
<li><a href="">#508</a><a href="">508</a>: Bump vite to 8.0.14 to resolve security advisories</li>
<li><a href="">#513</a><a href="">513</a>: Centralize test action-input fixtures in a shared helper</li>
<li><a href="">#541</a><a href="">541</a>, <a href="">#551</a><a href="">551</a>: Bump codecov/codecov-action from 6 to 7</li>
<li><a href="">#544</a><a href="">544</a>: Bump vite in the npm_and_yarn group</li>
<li><a href="">#545</a><a href="">545</a>, <a href="">#552</a><a href="">552</a>, <a href="">#561</a><a href="">561</a>: Bump actions/checkout from 6.0.2 to 7.0.1</li>
<li><a href="">#546</a><a href="">546</a>, <a href="">#556</a><a href="">556</a>, <a href="">#566</a>[566]: Bump js-yaml from 4.1.1 to 5.2.3</li>
<li><a href="">#547</a><a href="">547</a>: Bump semver from 7.7.4 to 7.8.5</li>
<li><a href="">#549</a><a href="">549</a>, <a href="">#558</a><a href="">558</a>, <a href="">#572</a>[572], <a href="">#575</a>[575]: Bump the npm_and_yarn group (linkify-it, postcss, undici, brace-expansion, <code>@​vitest/mocker</code>, <code>@​vitest/coverage-v8</code>)</li>
<li><a href="">#550</a><a href="">550</a>, <a href="">#557</a><a href="">557</a>: Bump marocchino/sticky-pull-request-comment from 3.0.3 to 3.0.5</li>
<li><a href="">#553</a><a href="">553</a>: Bump actions/cache from 5.0.5 to 6.1.0</li>
<li><a href="">#554</a><a href="">554</a>, <a href="">#560</a><a href="">560</a>, <a href="">#565</a>[565], <a href="">#574</a>[574]: Bump zizmorcore/zizmor-action from 0.5.6 to 0.6.3</li>
<li><a href="">#562</a>[562]: Bump actions/setup-node from 6.4.0 to 7.0.0</li>
<li><a href="">#573</a>[573]: Bump actions/deploy-pages from 5.0.0 to 5.0.1</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/conda-incubator/setup-miniconda/blob/main/CHANGELOG.md">conda-incubator/setup-miniconda's changelog</a>.</em></p>
<blockquote>
<h1>CHANGELOG</h1>
<h2><a href="https://github.com/conda-incubator/setup-miniconda/releases/tag/v4.1.0">v4.1.0</a> (2026-09-16)</h2>
<h3>Features and Enhancements</h3>
<ul>
<li><a href="">#567</a>[567]: Add Miniforge support for <code>linux-riscv64</code></li>
</ul>
<h3>Fixes</h3>
<ul>
<li><a href="">#539</a><a href="">539</a>: Look up the tool cache by tool name to fix Miniconda3 cache
misses</li>
</ul>
<h3>Tasks and Maintenance</h3>
<ul>
<li><a href="">#507</a><a href="">507</a>: Harden GitHub Actions workflows and add zizmor scanning</li>
<li><a href="">#508</a><a href="">508</a>: Bump vite to 8.0.14 to resolve security advisories</li>
<li><a href="">#513</a><a href="">513</a>: Centralize test action-input fixtures in a shared helper</li>
<li><a href="">#541</a><a href="">541</a>, <a href="">#551</a><a href="">551</a>: Bump codecov/codecov-action from 6 to 7</li>
<li><a href="">#544</a><a href="">544</a>: Bump vite in the npm_and_yarn group</li>
<li><a href="">#545</a><a href="">545</a>, <a href="">#552</a><a href="">552</a>, <a href="">#561</a>[561]: Bump actions/checkout from 6.0.2 to
7.0.1</li>
<li><a href="">#546</a><a href="">546</a>, <a href="">#556</a>[556], <a href="">#566</a>[566]: Bump js-yaml from 4.1.1 to 5.2.3</li>
<li><a href="">#547</a><a href="">547</a>: Bump semver from 7.7.4 to 7.8.5</li>
<li><a href="">#549</a><a href="">549</a>, <a href="">#558</a>[558], <a href="">#572</a>[572], <a href="">#575</a>[575]: Bump the npm_and_yarn
group (linkify-it, postcss, undici, brace-expansion, <code>@​vitest/mocker</code>,
<code>@​vitest/coverage-v8</code>)</li>
<li><a href="">#550</a><a href="">550</a>, <a href="">#557</a>[557]: Bump marocchino/sticky-pull-request-comment from
3.0.3 to 3.0.5</li>
<li><a href="">#553</a><a href="">553</a>: Bump actions/cache from 5.0.5 to 6.1.0</li>
<li><a href="">#554</a>[554], <a href="">#560</a>[560], <a href="">#565</a>[565], <a href="">#574</a>[574]: Bump
zizmorcore/zizmor-action from 0.5.6 to 0.6.3</li>
<li><a href="">#562</a>[562]: Bump actions/setup-node from 6.4.0 to 7.0.0</li>
<li><a href="">#573</a>[573]: Bump actions/deploy-pages from 5.0.0 to 5.0.1</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>be893c9</code></a> Prepare v4.1.0 release (<a href="">#576</a>)</li>
<li><a href=""><code>c7e9df3</code></a> Bump <code>@​vitest/mocker</code> from 4.1.0 to 5.0.1 in the npm_and_yarn group across 1 di...</li>
<li><a href=""><code>c9e4d79</code></a> Bump the npm_and_yarn group across 1 directory with 4 updates (<a href="">#572</a>)</li>
<li><a href=""><code>0ee587f</code></a> Add miniforge for linux-riscv64 (<a href="">#567</a>)</li>
<li><a href=""><code>8646c59</code></a> Bump zizmorcore/zizmor-action from 0.6.2 to 0.6.3 (<a href="">#574</a>)</li>
<li><a href=""><code>cdd7904</code></a> Bump actions/deploy-pages from 5.0.0 to 5.0.1 (<a href="">#573</a>)</li>
<li><a href=""><code>3770981</code></a> Bump js-yaml from 5.2.1 to 5.2.3 (<a href="">#566</a>)</li>
<li><a href=""><code>049518b</code></a> Bump zizmorcore/zizmor-action from 0.6.0 to 0.6.2 (<a href="">#565</a>)</li>
<li><a href=""><code>6dac52e</code></a> Bump actions/setup-node from 6.4.0 to 7.0.0 (<a href="">#562</a>)</li>
<li><a href=""><code>e81fd62</code></a> Bump zizmorcore/zizmor-action from 0.5.7 to 0.6.0 (<a href="">#560</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/conda-incubator/setup-miniconda/compare/8ee1f361103df19b6f8c8655fd3967a8ecb162d5...be893c923ea9cf1cf7cd510fbdde27c7e18cbdcb">compare view</a></li>
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

Updates `codecov/codecov-action` from 7.0.0 to 7.1.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/releases">codecov/codecov-action's releases</a>.</em></p>
<blockquote>
<h2>v7.1.1</h2>
<h2>What's Changed</h2>
<ul>
<li>chore(release): 7.1.1 by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1973</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v7.1.0...v7.1.1">https://github.com/codecov/codecov-action/compare/v7.1.0...v7.1.1</a></p>
<h2>v7.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li>chore(release): 7.1.0 by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1971</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v7.0.0...v7.1.0">https://github.com/codecov/codecov-action/compare/v7.0.0...v7.1.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>303a32d</code></a> chore(release): 7.1.1 (<a href="">#1973</a>)</li>
<li><a href=""><code>0b35c9e</code></a> chore(release): 7.1.0 (<a href="">#1971</a>)</li>
<li>See full diff in <a href="https://github.com/codecov/codecov-action/compare/fb8b3582c8e4def4969c97caa2f19720cb33a72f...303a32d7a59b442fa8d48b6a1cc6825c09c847a5">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `35a4dee11810`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.