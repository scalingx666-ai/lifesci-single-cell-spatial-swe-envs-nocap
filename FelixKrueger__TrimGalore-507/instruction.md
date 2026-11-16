# Issue

**Title:** build(deps): bump the github-actions-patch-minor group across 1 directory with 9 updates

## Description

Bumps the github-actions-patch-minor group with 9 updates in the / directory:

| Package | From | To |
| --- | --- | --- |
| [actions/setup-node](https://github.com/actions/setup-node) | `7.0.0` | `7.1.0` |
| [actions/upload-artifact](https://github.com/actions/upload-artifact) | `7.0.1` | `7.0.2` |
| [conda-incubator/setup-miniconda](https://github.com/conda-incubator/setup-miniconda) | `4.0.1` | `4.1.0` |
| [actions/deploy-pages](https://github.com/actions/deploy-pages) | `5.0.0` | `5.0.1` |
| [actions/download-artifact](https://github.com/actions/download-artifact) | `8.0.1` | `8.0.2` |
| [docker/setup-buildx-action](https://github.com/docker/setup-buildx-action) | `4.2.0` | `4.4.1` |
| [docker/login-action](https://github.com/docker/login-action) | `4.6.0` | `4.7.0` |
| [docker/build-push-action](https://github.com/docker/build-push-action) | `7.3.0` | `7.4.0` |
| [rust-lang/crates-io-auth-action](https://github.com/rust-lang/crates-io-auth-action) | `1.0.5` | `1.0.6` |

Updates `actions/setup-node` from 7.0.0 to 7.1.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-node/releases">actions/setup-node's releases</a>.</em></p>
<blockquote>
<h2>v7.1.0</h2>
<h2>What's Changed</h2>
<h3>Enhancements:</h3>
<ul>
<li>Add support for mise.toml file by <a href="https://github.com/gperdomor"><code>@​gperdomor</code></a> in <a href="">actions/setup-node#1421</a></li>
<li>Support absolute paths in node-version-file by <a href="https://github.com/v-mahabaleshwars"><code>@​v-mahabaleshwars</code></a> in <a href="">actions/setup-node#1633</a></li>
</ul>
<h3>Bug fixes:</h3>
<ul>
<li>Add Node version validation and manifest fetch retry by <a href="https://github.com/v-jitenderpalsingh"><code>@​v-jitenderpalsingh</code></a> in <a href="">actions/setup-node#1580</a></li>
</ul>
<h3>Documentation updates:</h3>
<ul>
<li>README.md: bump actions/checkout to latest version 7 by <a href="https://github.com/deining"><code>@​deining</code></a> in <a href="">actions/setup-node#1578</a></li>
<li>docs: add V7 ESM migration and NODE_AUTH_TOKEN behavior change by <a href="https://github.com/v-gowridurgad"><code>@​v-gowridurgad</code></a> in <a href="">actions/setup-node#1593</a></li>
<li>Fixed cache recommendation syntax by <a href="https://github.com/SubJunk"><code>@​SubJunk</code></a> in <a href="">actions/setup-node#1603</a></li>
</ul>
<h3>Dependency updates:</h3>
<ul>
<li>Update workflow pins and migrate Node matrices to modern versions by <a href="https://github.com/v-HarithaVattikuti"><code>@​v-HarithaVattikuti</code></a> in <a href="">actions/setup-node#1583</a></li>
<li>Upgrade  <code>@​actions/cache</code> to 6.2.0 by <a href="https://github.com/philip-gai"><code>@​philip-gai</code></a> in <a href="">actions/setup-node#1584</a></li>
<li>Pin <code>@​types/node</code> to v24 by <a href="https://github.com/v-priyagupta108"><code>@​v-priyagupta108</code></a> in <a href="">actions/setup-node#1585</a></li>
<li>Override brace-expansion to 5.0.8 by <a href="https://github.com/v-priyagupta108"><code>@​v-priyagupta108</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-node#1599</a></li>
<li>Upgrade  actions/checkout from 7.0.0 to 7.0.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1598</a></li>
<li>Upgrade  prettier from 3.8.4 to 3.9.6 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1590</a></li>
<li>Upgrade  <code>@​vercel/ncc</code> from 0.44.0 to 0.45.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1610</a></li>
<li>Upgrade  pnpm/action-setup from 6.0.9 to 6.0.10 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1602</a></li>
<li>Upgrade  baseline-browser-mapping from 2.10.38 to 2.11.22 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1629</a></li>
<li>Upgrade <code>@​types/semver</code> from 7.7.1 to 7.8.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1616</a></li>
<li>Upgrade <code>@​typescript-eslint/parser</code> from 8.62.0 to 8.70.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1615</a></li>
<li>Upgrade pnpm/action-setup from 6.0.10 to 6.1.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1631</a></li>
<li>Upgrade jest-each from 30.4.1 to 30.5.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1636</a></li>
<li>Upgrade eslint-plugin-n from 18.1.0 to 18.3.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1638</a></li>
<li>Update dependencies and add license files by <a href="https://github.com/v-HarithaVattikuti"><code>@​v-HarithaVattikuti</code></a> in <a href="">actions/setup-node#1642</a></li>
<li>Upgrade eslint from 10.5.0 to 10.11.0 and package.json from 7.0.0 to 7.1.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-node#1635</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/v-jitenderpalsingh"><code>@​v-jitenderpalsingh</code></a> made their first contribution in <a href="">actions/setup-node#1580</a></li>
<li><a href="https://github.com/philip-gai"><code>@​philip-gai</code></a> made their first contribution in <a href="">actions/setup-node#1584</a></li>
<li><a href="https://github.com/gperdomor"><code>@​gperdomor</code></a> made their first contribution in <a href="">actions/setup-node#1421</a></li>
<li><a href="https://github.com/SubJunk"><code>@​SubJunk</code></a> made their first contribution in <a href="">actions/setup-node#1603</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-node/compare/v7.0.0...v7.1.0">https://github.com/actions/setup-node/compare/v7.0.0...v7.1.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>949feb2</code></a> Bump eslint from 10.5.0 to 10.11.0 and package.json from 7.0.0 to 7.1.0 (<a href="">#1635</a>)</li>
<li><a href=""><code>7207c4f</code></a> chore: update dependencies and add license files (<a href="">#1642</a>)</li>
<li><a href=""><code>54337e0</code></a> Bump eslint-plugin-n from 18.1.0 to 18.3.0 (<a href="">#1638</a>)</li>
<li><a href=""><code>fb54fa8</code></a> Bump jest-each from 30.4.1 to 30.5.2 (<a href="">#1636</a>)</li>
<li><a href=""><code>7f84f1d</code></a> Bump pnpm/action-setup from 6.0.10 to 6.1.0 (<a href="">#1631</a>)</li>
<li><a href=""><code>0c54c7b</code></a> Bump <code>@​typescript-eslint/parser</code> from 8.62.0 to 8.70.0 (<a href="">#1615</a>)</li>
<li><a href=""><code>a829419</code></a> Bump <code>@​types/semver</code> from 7.7.1 to 7.8.0 (<a href="">#1616</a>)</li>
<li><a href=""><code>680d1e4</code></a> Support absolute paths in node-version-file (<a href="">#1633</a>)</li>
<li><a href=""><code>db0fb3a</code></a> Bump baseline-browser-mapping from 2.10.38 to 2.11.22 (<a href="">#1629</a>)</li>
<li><a href=""><code>94196ee</code></a> Bump pnpm/action-setup from 6.0.9 to 6.0.10 (<a href="">#1602</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/setup-node/compare/820762786026740c76f36085b0efc47a31fe5020...949feb2413d6458794dcd2491c4babbbce0c15c1">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/upload-artifact` from 7.0.1 to 7.0.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/upload-artifact/releases">actions/upload-artifact's releases</a>.</em></p>
<blockquote>
<h2>v7.0.2</h2>
<h2>What's Changed</h2>
<ul>
<li>Improves artifact download retries when the service returns HTTP 429 (rate limiting), including honoring valid Retry-After headers.</li>
<li>Updates <code>@​actions/artifact</code> to v6.3.1.</li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/tunc-d"><code>@​tunc-d</code></a> made their first contribution in <a href="">actions/upload-artifact#821</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/upload-artifact/compare/v7.0.1...v7.0.2">https://github.com/actions/upload-artifact/compare/v7.0.1...v7.0.2</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cf430e0</code></a> Merge pull request <a href="">#822</a> from actions/tunc-d-prepare-upload-v7-0-2</li>
<li><a href=""><code>c2acded</code></a> chore: prepare v7.0.2 release</li>
<li><a href=""><code>4687c1b</code></a> Merge pull request <a href="">#821</a> from actions/tunc-d-upload-artifact-package-bump</li>
<li><a href=""><code>8cbe1be</code></a> Bump <code>@​actions/artifact</code> to 6.3.1</li>
<li>See full diff in <a href="https://github.com/actions/upload-artifact/compare/043fb46d1a93c77aae656e7c1c64a875d1fc6a0a...cf430e030ddbb5b0abf93d22962f4752f3646cd9">compare view</a></li>
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

Updates `actions/deploy-pages` from 5.0.0 to 5.0.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/deploy-pages/releases">actions/deploy-pages's releases</a>.</em></p>
<blockquote>
<h2>v5.0.1</h2>
<h1>Changelog</h1>
<ul>
<li>Add backoff and jitter to deployment polling <a href="https://github.com/yoannchaudet"><code>@​yoannchaudet</code></a> (<a href="">#444</a>)</li>
<li>Improve deployment request test coverage <a href="https://github.com/adwitiyagoyal"><code>@​adwitiyagoyal</code></a> (<a href="">#440</a>)</li>
</ul>
<hr />
<p>See details of <a href="https://github.com/actions/deploy-pages/compare/v5.0.0...v5.0.1">all code changes</a> since previous release.</p>
<p>:warning: For use with products other than GitHub.com, such as GitHub Enterprise Server, please consult the <a href="https://github.com/actions/deploy-pages/#compatibility">compatibility table</a>.</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>368f825</code></a> Merge pull request <a href="">#444</a> from actions/yoannchaudet-deployment-polling-backoff</li>
<li><a href=""><code>7e97763</code></a> Validate deployment polling intervals</li>
<li><a href=""><code>0143e11</code></a> Add backoff and jitter to deployment polling</li>
<li><a href=""><code>5e98f10</code></a> Merge pull request <a href="">#440</a> from actions/user/adwitiya</li>
<li><a href=""><code>8b0625a</code></a> Improve deployment request test coverage</li>
<li>See full diff in <a href="https://github.com/actions/deploy-pages/compare/cd2ce8fcbc39b97be8ca5fce6e763baed58fa128...368f82528645a54fb793d4d04e342629a3f51346">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/download-artifact` from 8.0.1 to 8.0.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/download-artifact/releases">actions/download-artifact's releases</a>.</em></p>
<blockquote>
<h2>v8.0.2</h2>
<h2>What's Changed</h2>
<ul>
<li>Update the readme by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/download-artifact#473</a></li>
<li>Improves artifact download retries when the service returns HTTP 429 (rate limiting), including honoring valid Retry-After headers.</li>
<li>Update <code>@​actions/artifact</code> to 6.3.1 by <a href="https://github.com/tunc-d"><code>@​tunc-d</code></a> in <a href="">actions/download-artifact#492</a></li>
<li>Prepare download-artifact v8.0.2 by <a href="https://github.com/tunc-d"><code>@​tunc-d</code></a> in <a href="">actions/download-artifact#493</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/tunc-d"><code>@​tunc-d</code></a> made their first contribution in <a href="">actions/download-artifact#492</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/download-artifact/compare/v8.0.1...v8.0.2">https://github.com/actions/download-artifact/compare/v8.0.1...v8.0.2</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9000827</code></a> Merge pull request <a href="">#493</a> from actions/tunc-d-prepare-download-v8-0-2</li>
<li><a href=""><code>e455989</code></a> Prepare download-artifact v8.0.2</li>
<li><a href=""><code>a00b90c</code></a> Merge pull request <a href="">#492</a> from actions/tunc-d-download-artifact-package-bump</li>
<li><a href=""><code>29bb7ce</code></a> Update <code>@​actions/artifact</code> to 6.3.1</li>
<li><a href=""><code>484a0b5</code></a> Update the readme (<a href="">#473</a>)</li>
<li>See full diff in <a href="https://github.com/actions/download-artifact/compare/3e5f45b2cfb9172054b4087a40e8e0b5a5461e7c...9000827ccba6bdab643e8b6fd33ac0654aef8333">compare view</a></li>
</ul>
</details>
<br />

Updates `docker/setup-buildx-action` from 4.2.0 to 4.4.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/setup-buildx-action/releases">docker/setup-buildx-action's releases</a>.</em></p>
<blockquote>
<h2>v4.4.1</h2>
<ul>
<li>Skip BuildKit image pre-pulls for explicit endpoints by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#624</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v4.4.0...v4.4.1">https://github.com/docker/setup-buildx-action/compare/v4.4.0...v4.4.1</a></p>
<h2>v4.4.0</h2>
<ul>
<li>Use official Buildx releases for cloud driver by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#606</a></li>
<li>Pull BuildKit image before builder creation by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#609</a></li>
<li>Use shared error helpers for Buildx and Docker commands by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#620</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.95.0 to 0.100.0 in <a href="">docker/setup-buildx-action#610</a> <a href="">docker/setup-buildx-action#618</a> <a href="">docker/setup-buildx-action#619</a></li>
<li>Bump <code>@​humanfs/node</code> from 0.16.7 to 0.16.8 in <a href="">docker/setup-buildx-action#614</a></li>
<li>Bump js-yaml from 5.3.0 to 5.4.2 in <a href="">docker/setup-buildx-action#608</a> <a href="">docker/setup-buildx-action#617</a></li>
<li>Bump postcss-selector-parser from 7.1.1 to 7.1.5 in <a href="">docker/setup-buildx-action#611</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v4.3.0...v4.4.0">https://github.com/docker/setup-buildx-action/compare/v4.3.0...v4.4.0</a></p>
<h2>v4.3.0</h2>
<ul>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.92.0 to 0.95.0 in <a href="">docker/setup-buildx-action#595</a></li>
<li>Bump brace-expansion from 1.1.13 to 1.1.18 in <a href="">docker/setup-buildx-action#600</a></li>
<li>Bump js-yaml from 5.2.0 to 5.3.0 in <a href="">docker/setup-buildx-action#585</a></li>
<li>Bump postcss from 8.5.10 to 8.5.25 in <a href="">docker/setup-buildx-action#598</a></li>
<li>Bump undici from 6.27.0 to 6.28.0 in <a href="">docker/setup-buildx-action#601</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v4.2.0...v4.3.0">https://github.com/docker/setup-buildx-action/compare/v4.2.0...v4.3.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>f87e599</code></a> Merge pull request <a href="">#624</a> from crazy-max/skip-pull-with-endpoint</li>
<li><a href=""><code>e700274</code></a> chore: update generated content</li>
<li><a href=""><code>3061c91</code></a> skip BuildKit image pre-pulls for explicit endpoints</li>
<li><a href=""><code>594f3bf</code></a> Merge pull request <a href="">#609</a> from crazy-max/pull-buildkit-image-before-create</li>
<li><a href=""><code>bd6e702</code></a> chore: update generated content</li>
<li><a href=""><code>6268c9d</code></a> pull BuildKit image before builder creation</li>
<li><a href=""><code>e823525</code></a> Merge pull request <a href="">#621</a> from docker/dependabot/github_actions/codeql-actions-...</li>
<li><a href=""><code>533ed8e</code></a> build(deps): bump the codeql-actions group with 2 updates</li>
<li><a href=""><code>bedaf13</code></a> Merge pull request <a href="">#620</a> from crazy-max/shared-error-helpers</li>
<li><a href=""><code>d5079fb</code></a> chore: update generated content</li>
<li>Additional commits viewable in <a href="https://github.com/docker/setup-buildx-action/compare/bb05f3f5519dd87d3ba754cc423b652a5edd6d2c...f87e5991a6d7451dcb8d9637bfbc97413f497069">compare view</a></li>
</ul>
</details>
<br />

Updates `docker/login-action` from 4.6.0 to 4.7.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/login-action/releases">docker/login-action's releases</a>.</em></p>
<blockquote>
<h2>v4.7.0</h2>
<ul>
<li>Preserve explicit ECR settings in <code>registry-auth</code> by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#1089</a></li>
<li>Use registry hosts for scoped credentials by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#1088</a></li>
<li>Raise Docker Hub OIDC max expiry to 6 hours by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#1068</a></li>
<li>Log Docker Hub OIDC token exchange progress by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#1061</a></li>
<li>Bump <code>@​aws-sdk/client-ecr</code> and <code>@​aws-sdk/client-ecr-public</code> to 3.1154.0 in <a href="">docker/login-action#1093</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.94.0 to 0.107.0 in <a href="">docker/login-action#1100</a></li>
<li>Bump <code>@​humanfs/node</code> from 0.16.7 to 0.16.8 in <a href="">docker/login-action#1077</a></li>
<li>Bump csv-parse from 7.0.1 to 7.0.3 in <a href="">docker/login-action#1078</a></li>
<li>Bump handlebars from 4.7.9 to 4.7.10 in <a href="">docker/login-action#1091</a></li>
<li>Bump js-yaml from 5.2.2 to 5.5.0 in <a href="">docker/login-action#1066</a></li>
<li>Bump postcss from 8.5.22 to 8.5.26 in <a href="">docker/login-action#1071</a></li>
<li>Bump postcss-selector-parser from 7.1.1 to 7.1.6 in <a href="">docker/login-action#1092</a></li>
<li>Bump source-map-js from 1.2.1 to 1.2.2 in <a href="">docker/login-action#1090</a></li>
<li>Bump undici from 6.27.0 to 6.29.1 in <a href="">docker/login-action#1085</a></li>
<li>Bump uuid from 14.0.1 to 14.0.3 in <a href="">docker/login-action#1096</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v4.6.0...v4.7.0">https://github.com/docker/login-action/compare/v4.6.0...v4.7.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>81c6f93</code></a> Merge pull request <a href="">#1100</a> from docker/dependabot/npm_and_yarn/docker/actions-t...</li>
<li><a href=""><code>1b16c8d</code></a> Merge pull request <a href="">#1096</a> from docker/dependabot/npm_and_yarn/uuid-14.0.3</li>
<li><a href=""><code>ac86b5e</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>1476d84</code></a> build(deps): bump <code>@​docker/actions-toolkit</code> from 0.94.0 to 0.107.0</li>
<li><a href=""><code>503cee6</code></a> Merge pull request <a href="">#1095</a> from docker/dependabot/github_actions/actions/create...</li>
<li><a href=""><code>f093535</code></a> Merge pull request <a href="">#1099</a> from docker/dependabot/github_actions/codecov/codeco...</li>
<li><a href=""><code>d5ae7f1</code></a> Merge pull request <a href="">#1098</a> from docker/dependabot/github_actions/docker/bake-ac...</li>
<li><a href=""><code>6f97507</code></a> Merge pull request <a href="">#1097</a> from docker/dependabot/github_actions/docker/bake-ac...</li>
<li><a href=""><code>006d61f</code></a> Merge pull request <a href="">#1094</a> from docker/dependabot/github_actions/codeql-actions...</li>
<li><a href=""><code>93f5f52</code></a> Merge pull request <a href="">#1093</a> from docker/dependabot/npm_and_yarn/aws-sdk-dependen...</li>
<li>Additional commits viewable in <a href="https://github.com/docker/login-action/compare/dbcb813823bdd20940b903addbd779551569679f...81c6f93d4bc991e510b342a00b419b3bb4efc5c6">compare view</a></li>
</ul>
</details>
<br />

Updates `docker/build-push-action` from 7.3.0 to 7.4.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/build-push-action/releases">docker/build-push-action's releases</a>.</em></p>
<blockquote>
<h2>v7.4.0</h2>
<ul>
<li>Use the shared error helper for Buildx commands by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/build-push-action#1620</a></li>
<li>Prevent workflow command injection in metadata logs by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/build-push-action#1617</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.92.0 to 0.100.0 in <a href="">docker/build-push-action#1614</a> <a href="">docker/build-push-action#1618</a> <a href="">docker/build-push-action#1621</a></li>
<li>Bump <code>@​humanfs/node</code> from 0.16.7 to 0.16.8 in <a href="">docker/build-push-action#1609</a></li>
<li>Bump brace-expansion from 1.1.13 to 1.1.18 in <a href="">docker/build-push-action#1592</a></li>
<li>Bump csv-parse from 7.0.0 to 7.0.2 in <a href="">docker/build-push-action#1613</a></li>
<li>Bump js-yaml from 4.3.0 to 4.3.2 in <a href="">docker/build-push-action#1605</a> <a href="">docker/build-push-action#1615</a></li>
<li>Bump nanoid from 3.3.16 to 3.3.18 in <a href="">docker/build-push-action#1611</a></li>
<li>Bump postcss from 8.5.10 to 8.5.25 in <a href="">docker/build-push-action#1590</a></li>
<li>Bump postcss-selector-parser from 7.1.1 to 7.1.5 in <a href="">docker/build-push-action#1606</a></li>
<li>Bump sigstore from 4.1.0 to 4.1.1 in <a href="">docker/build-push-action#1577</a></li>
<li>Bump undici from 6.27.0 to 6.28.0 in <a href="">docker/build-push-action#1594</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/build-push-action/compare/v7.3.0...v7.4.0">https://github.com/docker/build-push-action/compare/v7.3.0...v7.4.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c3c9e26</code></a> Merge pull request <a href="">#1621</a> from docker/dependabot/npm_and_yarn/docker/actions-t...</li>
<li><a href=""><code>459b674</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>4dedcb2</code></a> chore(deps): Bump <code>@​docker/actions-toolkit</code> from 0.99.0 to 0.100.0</li>
<li><a href=""><code>379bf63</code></a> Merge pull request <a href="">#1620</a> from crazy-max/buildx-error-message</li>
<li><a href=""><code>9877975</code></a> chore: update generated content</li>
<li><a href=""><code>7ed0556</code></a> use the shared Buildx error summary helper</li>
<li><a href=""><code>91670ba</code></a> Merge pull request <a href="">#1618</a> from docker/dependabot/npm_and_yarn/docker/actions-t...</li>
<li><a href=""><code>80dbc86</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>50cac3a</code></a> chore(deps): Bump <code>@​docker/actions-toolkit</code> from 0.98.0 to 0.99.0</li>
<li><a href=""><code>03b4d6c</code></a> Merge pull request <a href="">#1617</a> from crazy-max/fix-metadata-workflow-commands</li>
<li>Additional commits viewable in <a href="https://github.com/docker/build-push-action/compare/53b7df96c91f9c12dcc8a07bcb9ccacbed38856a...c3c9e263c25d99ce0380d002d59b67737d91b0dc">compare view</a></li>
</ul>
</details>
<br />

Updates `rust-lang/crates-io-auth-action` from 1.0.5 to 1.0.6
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/crates-io-auth-action/releases">rust-lang/crates-io-auth-action's releases</a>.</em></p>
<blockquote>
<h2>v1.0.6</h2>
<h2>What's Changed</h2>
<p>update dependencies</p>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/crates-io-auth-action/compare/v1.0.5...v1.0.6">https://github.com/rust-lang/crates-io-auth-action/compare/v1.0.5...v1.0.6</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>3268eb4</code></a> Merge pull request <a href="">#278</a> from marcoienibot/chore/update-dependencies-2026-10</li>
<li><a href=""><code>e901356</code></a> chore(deps): update dependencies and GitHub Actions</li>
<li><a href=""><code>9c067fc</code></a> Merge pull request <a href="">#277</a> from rust-lang/renovate/msw-3.x</li>
<li><a href=""><code>9b55005</code></a> chore(deps): update dependency msw to v3</li>
<li><a href=""><code>4920f09</code></a> Merge pull request <a href="">#276</a> from rust-lang/renovate/major-github-actions</li>
<li><a href=""><code>04dcccb</code></a> chore(deps): update github actions</li>
<li><a href=""><code>82864bf</code></a> Merge pull request <a href="">#274</a> from rust-lang/renovate/major-vitest-monorepo</li>
<li><a href=""><code>2bd8e07</code></a> chore(deps): update dependency vitest to v5</li>
<li><a href=""><code>f14f407</code></a> Merge pull request <a href="">#271</a> from rust-lang/renovate/github-actions</li>
<li><a href=""><code>0205d6c</code></a> chore(deps): update github actions</li>
<li>Additional commits viewable in <a href="https://github.com/rust-lang/crates-io-auth-action/compare/c6f97d42243bad5fab37ca0427f495c86d5b1a18...3268eb413133e2960fa4ae0e963ca76380c54cd9">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `630315276ce1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.