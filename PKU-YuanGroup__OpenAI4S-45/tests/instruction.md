# Issue

**Title:** chore(deps): bump the workflow-actions group across 1 directory with 6 updates

## Description

Bumps the workflow-actions group with 6 updates in the / directory:

| Package | From | To |
| --- | --- | --- |
| [actions/checkout](https://github.com/actions/checkout) | `4.4.0` | `7.0.1` |
| [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv) | `5.4.2` | `9.0.0` |
| [actions/setup-python](https://github.com/actions/setup-python) | `5.6.0` | `7.0.0` |
| [actions/setup-node](https://github.com/actions/setup-node) | `4.4.0` | `7.0.0` |
| [ossf/scorecard-action](https://github.com/ossf/scorecard-action) | `2.4.3` | `2.4.4` |
| [github/codeql-action/upload-sarif](https://github.com/github/codeql-action) | `4.37.0` | `4.37.3` |

Updates `actions/checkout` from 4.4.0 to 7.0.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/releases">actions/checkout's releases</a>.</em></p>
<blockquote>
<h2>v7.0.1</h2>
<h2>What's Changed</h2>
<ul>
<li>skip running unsafe pr check if input is default by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2518</a></li>
<li>trim only ascii whitespace for branch by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2521</a></li>
<li>escape values passed to --unset by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2530</a></li>
<li>Various dependency updates</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v7...v7.0.1">https://github.com/actions/checkout/compare/v7...v7.0.1</a></p>
<h2>v7.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>block checking out fork pr for pull_request_target and workflow_run by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2454</a></li>
<li>Bump actions/publish-immutable-action from 0.0.3 to 0.0.4 in the minor-actions-dependencies group across 1 directory by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/checkout#2458</a></li>
<li>Bump flatted from 3.3.1 to 3.4.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/checkout#2460</a></li>
<li>Bump js-yaml from 4.1.0 to 4.2.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/checkout#2461</a></li>
<li>Bump <code>@​actions/core</code> and <code>@​actions/tool-cache</code> and Remove uuid by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/checkout#2459</a></li>
<li>upgrade module to esm and update dependencies by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2463</a></li>
<li>Bump the minor-npm-dependencies group across 1 directory with 3 updates by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/checkout#2462</a></li>
<li>getting ready for checkout v7 release by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2464</a></li>
<li>update error wording by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2467</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> made their first contribution in <a href="">actions/checkout#2454</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v6.0.3...v7.0.0">https://github.com/actions/checkout/compare/v6.0.3...v7.0.0</a></p>
<h2>v6.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li><strong>[BREAKING]</strong> backport <code>allow-unsafe-pr-checkout</code> to v6 by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2500</a></li>
<li>backport fixes to releases-v6 by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2527</a></li>
</ul>
<p><a href="https://github.blog/changelog/2026-06-18-safer-pull_request_target-defaults-for-github-actions-checkout/">https://github.blog/changelog/2026-06-18-safer-pull_request_target-defaults-for-github-actions-checkout/</a> for more details about this breaking change</p>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v6.0.3...v6.1.0">https://github.com/actions/checkout/compare/v6.0.3...v6.1.0</a></p>
<h2>v6.0.3</h2>
<h2>What's Changed</h2>
<ul>
<li>Update changelog by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2357</a></li>
<li>fix: expand merge commit SHA regex and add SHA-256 test cases by <a href="https://github.com/yaananth"><code>@​yaananth</code></a> in <a href="">actions/checkout#2414</a></li>
<li>Fix checkout init for SHA-256 repositories by <a href="https://github.com/yaananth"><code>@​yaananth</code></a> in <a href="">actions/checkout#2439</a></li>
<li>Update changelog for v6.0.3 by <a href="https://github.com/yaananth"><code>@​yaananth</code></a> in <a href="">actions/checkout#2446</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/yaananth"><code>@​yaananth</code></a> made their first contribution in <a href="">actions/checkout#2414</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v6...v6.0.3">https://github.com/actions/checkout/compare/v6...v6.0.3</a></p>
<h2>v6.0.2</h2>
<h2>What's Changed</h2>
<ul>
<li>Add orchestration_id to git user-agent when ACTIONS_ORCHESTRATION_ID is set by <a href="https://github.com/TingluoHuang"><code>@​TingluoHuang</code></a> in <a href="">actions/checkout#2355</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/blob/main/CHANGELOG.md">actions/checkout's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<h2>v7.0.1</h2>
<ul>
<li>Skip running unsafe pr check if input is default by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2518</a></li>
<li>Trim only ascii whitespace for branch by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2521</a></li>
<li>Escape values passed to --unset by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2530</a></li>
<li>Various dependency updates</li>
</ul>
<h2>v7.0.0</h2>
<ul>
<li>Block checking out fork PR for pull_request_target and workflow_run by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2454</a></li>
<li>Various dependency updates</li>
</ul>
<h2>v6.0.3</h2>
<ul>
<li>Fix checkout init for SHA-256 repositories by <a href="https://github.com/yaananth"><code>@​yaananth</code></a> in <a href="">actions/checkout#2439</a></li>
<li>fix: expand merge commit SHA regex and add SHA-256 test cases by <a href="https://github.com/yaananth"><code>@​yaananth</code></a> in <a href="">actions/checkout#2414</a></li>
</ul>
<h2>v6.0.2</h2>
<ul>
<li>Fix tag handling: preserve annotations and explicit fetch-tags by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2356</a></li>
</ul>
<h2>v6.0.1</h2>
<ul>
<li>Add worktree support for persist-credentials includeIf by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2327</a></li>
</ul>
<h2>v6.0.0</h2>
<ul>
<li>Persist creds to a separate file by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2286</a></li>
<li>Update README to include Node.js 24 support details and requirements by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2248</a></li>
</ul>
<h2>v5.0.1</h2>
<ul>
<li>Port v6 cleanup to v5 by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2301</a></li>
</ul>
<h2>v5.0.0</h2>
<ul>
<li>Update actions checkout to use node 24 by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2226</a></li>
</ul>
<h2>v4.3.1</h2>
<ul>
<li>Port v6 cleanup to v4 by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2305</a></li>
</ul>
<h2>v4.3.0</h2>
<ul>
<li>docs: update README.md by <a href="https://github.com/motss"><code>@​motss</code></a> in <a href="">actions/checkout#1971</a></li>
<li>Add internal repos for checking out multiple repositories by <a href="https://github.com/mouismail"><code>@​mouismail</code></a> in <a href="">actions/checkout#1977</a></li>
<li>Documentation update - add recommended permissions to Readme by <a href="https://github.com/benwells"><code>@​benwells</code></a> in <a href="">actions/checkout#2043</a></li>
<li>Adjust positioning of user email note and permissions heading by <a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> in <a href="">actions/checkout#2044</a></li>
<li>Update README.md by <a href="https://github.com/nebuk89"><code>@​nebuk89</code></a> in <a href="">actions/checkout#2194</a></li>
<li>Update CODEOWNERS for actions by <a href="https://github.com/TingluoHuang"><code>@​TingluoHuang</code></a> in <a href="">actions/checkout#2224</a></li>
<li>Update package dependencies by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2236</a></li>
</ul>
<h2>v4.2.2</h2>
<ul>
<li><code>url-helper.ts</code> now leverages well-known environment variables by <a href="https://github.com/jww3"><code>@​jww3</code></a> in <a href="">actions/checkout#1941</a></li>
<li>Expand unit test coverage for <code>isGhes</code> by <a href="https://github.com/jww3"><code>@​jww3</code></a> in <a href="">actions/checkout#1946</a></li>
</ul>
<h2>v4.2.1</h2>
<ul>
<li>Check out other refs/* by commit if provided, fall back to ref by <a href="https://github.com/orhantoy"><code>@​orhantoy</code></a> in <a href="">actions/checkout#1924</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>3d3c42e</code></a> prep v7.0.1 release (<a href="">#2531</a>)</li>
<li><a href=""><code>2880268</code></a> escape values passed to --unset (<a href="">#2530</a>)</li>
<li><a href=""><code>12cd223</code></a> trim only ascii whitespace for branch (<a href="">#2521</a>)</li>
<li><a href=""><code>62661c4</code></a> skip running unsafe pr check if input is default (<a href="">#2518</a>)</li>
<li><a href=""><code>e8d4307</code></a> Bump the minor-actions-dependencies group with 2 updates (<a href="">#2499</a>)</li>
<li><a href=""><code>631c942</code></a> eslint 9 (<a href="">#2474</a>)</li>
<li><a href=""><code>4f1f4ae</code></a> Bump actions/upload-artifact from 4 to 7 (<a href="">#2476</a>)</li>
<li><a href=""><code>ba09753</code></a> Bump actions/checkout from 6 to 7 (<a href="">#2488</a>)</li>
<li><a href=""><code>b9e0990</code></a> Bump docker/login-action from 3.3.0 to 4.2.0 (<a href="">#2479</a>)</li>
<li><a href=""><code>e8cb398</code></a> Bump docker/build-push-action from 6.5.0 to 7.2.0 (<a href="">#2478</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/checkout/compare/v4.4.0...3d3c42e5aac5ba805825da76410c181273ba90b1">compare view</a></li>
</ul>
</details>
<br />

Updates `astral-sh/setup-uv` from 5.4.2 to 9.0.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/setup-uv/releases">astral-sh/setup-uv's releases</a>.</em></p>
<blockquote>
<h2>v9.0.0 🌈 Change <code>prune-cache</code> default to <code>false</code></h2>
<h2>Changes</h2>
<p>This release disables the default cache cache pruning to ease the load on the PyPi infrastructure.
Since users might experience more GitHub Actions cache usage which might result in higher costs this is marked as a breaking change. To read more on why we did this (now) you can read the detailed analysis and reasoning in <a href="">#967</a></p>
<p>Besides this big breaking change we also have a small bugfix while building caches for linux distributions that behave a big different than the &quot;big ones&quot; and a speed up in version resolution by only reading the version manifest until a matching version is found saving runtime and network bandwith.</p>
<h2>🚨 Breaking changes</h2>
<ul>
<li>Change <code>prune-cache</code> default to <code>false</code> <a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a> (<a href="">#967</a>)</li>
</ul>
<h2>🐛 Bug fixes</h2>
<ul>
<li>fix: fall back to distribution ID when os-release has no version field <a href="https://github.com/cxzhong"><code>@​cxzhong</code></a> (<a href="">#961</a>)</li>
</ul>
<h2>🚀 Enhancements</h2>
<ul>
<li>Speed up version client by partial response reads <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#807</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.11.30 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#968</a>)</li>
<li>chore: update known checksums for 0.11.29 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#960</a>)</li>
</ul>
<h2>📚 Documentation</h2>
<ul>
<li>docs: update version references to v8.3.2 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#949</a>)</li>
</ul>
<h2>⬆️ Dependency updates</h2>
<ul>
<li>chore(deps): roll up Dependabot updates <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#970</a>)</li>
<li>chore(deps): roll up Dependabot updates <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#962</a>)</li>
</ul>
<h2>v8.2.0 🌈 New inputs <code>quiet</code> and <code>download-from-astral-mirror</code></h2>
<h2>Changes</h2>
<p>This release brings two new inputs and a few bug fixes.</p>
<h3>New inputs</h3>
<p>Lets talk about the new inputs first.</p>
<h4>quiet</h4>
<p>Pretty simple. It turns of all <code>info</code> loggings. Useful if you use this in a composite action and are not interested in all the details.
In the upcoming releases we will add log groups to fully implement support for &quot;less noise&quot;</p>
<blockquote>
<p>[!NOTE]<br />
Warnings and errors are always logged.</p>
</blockquote>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c771a70</code></a> chore(deps): roll up Dependabot updates (<a href="">#970</a>)</li>
<li><a href=""><code>2f537ca</code></a> chore: update known checksums for 0.11.30 (<a href="">#968</a>)</li>
<li><a href=""><code>2269552</code></a> Speed up version client by partial response reads (<a href="">#807</a>)</li>
<li><a href=""><code>47a7f4f</code></a> Change <code>prune-cache</code> default to <code>false</code> (<a href="">#967</a>)</li>
<li><a href=""><code>71966ef</code></a> chore(deps): roll up Dependabot updates (<a href="">#962</a>)</li>
<li><a href=""><code>f12b1f0</code></a> fix: fall back to distribution ID when os-release has no version field (<a href="">#961</a>)</li>
<li><a href=""><code>ecd24dd</code></a> chore: update known checksums for 0.11.29 (<a href="">#960</a>)</li>
<li><a href=""><code>6a19136</code></a> docs: update version references to v8.3.2 (<a href="">#949</a>)</li>
<li><a href=""><code>11f9893</code></a> chore: roll up Dependabot updates (<a href="">#948</a>)</li>
<li><a href=""><code>f798556</code></a> docs: update version references to v8.3.1 (<a href="">#946</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/setup-uv/compare/v5.4.2...c771a70e6277c0a99b617c7a806ffedaca235ff9">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/setup-python` from 5.6.0 to 7.0.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>v7.0.0</h2>
<h2>What's Changed</h2>
<h3>Enhancements</h3>
<ul>
<li>Migrate to ESM and upgrade dependencies by <a href="https://github.com/priyagupta108"><code>@​priyagupta108</code></a> in <a href="">actions/setup-python#1330</a></li>
<li>Pin SHA commits and update docs with latest versions by <a href="https://github.com/HarithaVattikuti"><code>@​HarithaVattikuti</code></a> in <a href="">actions/setup-python#1338</a></li>
<li>Remove the pip-install input by <a href="https://github.com/gowridurgad"><code>@​gowridurgad</code></a> in <a href="">actions/setup-python#1336</a></li>
</ul>
<h3>Bug Fix</h3>
<ul>
<li>Fix to Classify stderr warning messages as warnings instead of errors in annotations by <a href="https://github.com/lmvysakh"><code>@​lmvysakh</code></a> in <a href="">actions/setup-python#1335</a></li>
<li>Validate and retry manifest fetch to prevent silent failures by <a href="https://github.com/priyagupta108"><code>@​priyagupta108</code></a> in <a href="">actions/setup-python#1332</a></li>
</ul>
<h3>Dependency Upgrade</h3>
<ul>
<li>Bump certifi from 2020.6.20 to 2024.7.4 in /<strong>tests</strong>/data by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-python#1328</a></li>
<li>Remove EOL Python versions and Bumps numpy text fixture by <a href="https://github.com/priya-kinthali"><code>@​priya-kinthali</code></a> in <a href="">actions/setup-python#1333</a></li>
<li>Upgrade <code>@​actions/cache</code> to 6.2.0 by <a href="https://github.com/philip-gai"><code>@​philip-gai</code></a> in <a href="">actions/setup-python#1337</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/lmvysakh"><code>@​lmvysakh</code></a> made their first contribution in <a href="">actions/setup-python#1335</a></li>
<li><a href="https://github.com/philip-gai"><code>@​philip-gai</code></a> made their first contribution in <a href="">actions/setup-python#1337</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-python/compare/v6...v7.0.0">https://github.com/actions/setup-python/compare/v6...v7.0.0</a></p>
<h2>v6.3.0</h2>
<h2>What's Changed</h2>
<h3>Enhancement</h3>
<ul>
<li>Add RHEL support and include Linux distro in cache keys by <a href="https://github.com/priyagupta108"><code>@​priyagupta108</code></a> in <a href="">actions/setup-python#1323</a></li>
<li>Fix pip cache error handling on Windows by <a href="https://github.com/priyagupta108"><code>@​priyagupta108</code></a> in <a href="">actions/setup-python#1040</a></li>
</ul>
<h3>Dependency update</h3>
<ul>
<li>Upgrade minimatch from 3.1.2 to 3.1.5 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-python#1281</a></li>
<li>Upgrade actions dependencies by <a href="https://github.com/gowridurgad"><code>@​gowridurgad</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-python#1303</a></li>
<li>Upgrade <code>@​actions/cache</code> to 5.1.0, log cache write denied by <a href="https://github.com/jasongin"><code>@​jasongin</code></a> in <a href="">actions/setup-python#1324</a></li>
<li>Upgrade dependency versions and test workflow configuration by <a href="https://github.com/HarithaVattikuti"><code>@​HarithaVattikuti</code></a> in <a href="">actions/setup-python#1322</a></li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Update advanced-usage.md by <a href="https://github.com/Dunky-Z"><code>@​Dunky-Z</code></a> in <a href="">actions/setup-python#811</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/gowridurgad"><code>@​gowridurgad</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> made their first contribution in <a href="">actions/setup-python#1303</a></li>
<li><a href="https://github.com/jasongin"><code>@​jasongin</code></a> made their first contribution in <a href="">actions/setup-python#1324</a></li>
<li><a href="https://github.com/Dunky-Z"><code>@​Dunky-Z</code></a> made their first contribution in <a href="">actions/setup-python#811</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-python/compare/v6.2.0...v6.3.0">https://github.com/actions/setup-python/compare/v6.2.0...v6.3.0</a></p>
<h2>v6.2.0</h2>
<h2>What's Changed</h2>
<h3>Dependency Upgrades</h3>
<ul>
<li>Upgrade dependencies to Node 24 compatible versions by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/setup-python#1259</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5fda3b9</code></a> Pin SHA commits and update docs with latest versions (<a href="">#1338</a>)</li>
<li><a href=""><code>4ab7e95</code></a> Merge pull request <a href="">#1337</a> from actions/philip-gai/bump-actions-cache-6-2-0</li>
<li><a href=""><code>0f3a009</code></a> Remove the pip-install input (<a href="">#1336</a>)</li>
<li><a href=""><code>f8cf429</code></a> Migrate to ESM and upgrade dependencies (<a href="">#1330</a>)</li>
<li><a href=""><code>54baeea</code></a> Validate and retry manifest fetch to prevent silent failures (<a href="">#1332</a>)</li>
<li><a href=""><code>c709277</code></a> Annotation code fix (<a href="">#1335</a>)</li>
<li><a href=""><code>6849080</code></a> remove EOL Python versions and Bumps numpy text fixture (<a href="">#1333</a>)</li>
<li><a href=""><code>0903b46</code></a> Bump certifi from 2020.6.20 to 2024.7.4 in /<strong>tests</strong>/data (<a href="">#1328</a>)</li>
<li><a href=""><code>ece7cb0</code></a> Fix pip cache error handling on Windows. (<a href="">#1040</a>)</li>
<li><a href=""><code>1d18d7a</code></a> Update advanced-usage.md (<a href="">#811</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/setup-python/compare/a26af69be951a213d495a4c3e4e4022e16d87065...5fda3b95a4ea91299a34e894583c3862153e4b97">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/setup-node` from 4.4.0 to 7.0.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-node/releases">actions/setup-node's releases</a>.</em></p>
<blockquote>
<h2>v7.0.0</h2>
<h2>What's Changed</h2>
<h3>Enhancements:</h3>
<ul>
<li>Add cache-primary-key and cache-matched-key as outputs by <a href="https://github.com/gowridurgad"><code>@​gowridurgad</code></a> in <a href="">actions/setup-node#1577</a></li>
<li>Migrate to ESM and upgrade dependencies by <a href="https://github.com/gowridurgad"><code>@​gowridurgad</code></a> in <a href="">actions/setup-node#1574</a></li>
</ul>
<h3>Bug fixes:</h3>
<ul>
<li>Remove dummy NODE_AUTH_TOKEN export by <a href="https://github.com/gowridurgad"><code>@​gowridurgad</code></a> in <a href="">actions/setup-node#1558</a></li>
<li>Only use <code>mirrorToken</code> in <code>getManifest</code> if it's provided by <a href="https://github.com/deiga"><code>@​deiga</code></a> in <a href="">actions/setup-node#1548</a></li>
</ul>
<h3>Documentation updates:</h3>
<ul>
<li>Add documentation for publishing to npm with Trusted Publisher (OIDC) by <a href="https://github.com/chiranjib-swain"><code>@​chiranjib-swain</code></a> in <a href="">actions/setup-node#1536</a></li>
<li>docs: Update restore-only cache documentation by <a href="https://github.com/priya-kinthali"><code>@​priya-kinthali</code></a> in <a href="">actions/setup-node#1550</a></li>
<li>docs: Update caching recommendations to mitigate cache poisoning risks by <a href="https://github.com/chiranjib-swain"><code>@​chiranjib-swain</code></a> in <a href="">actions/setup-node#1567</a></li>
</ul>
<h3>Dependency update:</h3>
<ul>
<li>Upgrade <code>@​actions/cache</code> to 5.1.0, log cache write denied by <a href="https://github.com/jasongin"><code>@​jasongin</code></a> in <a href="">actions/setup-node#1569</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/chiranjib-swain"><code>@​chiranjib-swain</code></a> made their first contribution in <a href="">actions/setup-node#1536</a></li>
<li><a href="https://github.com/deiga"><code>@​deiga</code></a> made their first contribution in <a href="">actions/setup-node#1548</a></li>
<li><a href="https://github.com/jasongin"><code>@​jasongin</code></a> made their first contribution in <a href="">actions/setup-node#1569</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-node/compare/v6...v7.0.0">https://github.com/actions/setup-node/compare/v6...v7.0.0</a></p>
<h2>v6.5.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update <code>@​actions/cache</code> to 5.1.0 and add security overrides for undici and fast-xml-parser by <a href="https://github.com/HarithaVattikuti"><code>@​HarithaVattikuti</code></a> in <a href="">actions/setup-node#1579</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-node/compare/v6.4.0...v6.5.0">https://github.com/actions/setup-node/compare/v6.4.0...v6.5.0</a></p>
<h2>v6.4.0</h2>
<h2>What's Changed</h2>
<h3>Dependency updates:</h3>
<ul>
<li>Upgrade <a href="https://github.com/actions"><code>@​actions</code></a> dependencies by <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-node#1525</a></li>
<li>Update Node.js versions in versions.yml and bump package to v6.4.0  by <a href="https://github.com/priya-kinthali"><code>@​priya-kinthali</code></a> in <a href="">actions/setup-node#1533</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/Copilot"><code>@​Copilot</code></a> made their first contribution in <a href="">actions/setup-node#1525</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-node/compare/v6...v6.4.0">https://github.com/actions/setup-node/compare/v6...v6.4.0</a></p>
<h2>v6.3.0</h2>
<h2>What's Changed</h2>
<h3>Enhancements:</h3>
<ul>
<li>Support parsing <code>devEngines</code> field by <a href="https://github.com/susnux"><code>@​susnux</code></a> in <a href="">actions/setup-node#1283</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8207627</code></a> Migrate to ESM and upgrade dependencies (<a href="">#1574</a>)</li>
<li><a href=""><code>04be95c</code></a> Add cache-primary-key and cache-matched-key as outputs (<a href="">#1577</a>)</li>
<li><a href=""><code>7c2c68d</code></a> docs: Update caching recommendations to mitigate cache poisoning risks (<a href="">#1567</a>)</li>
<li><a href=""><code>6a61c03</code></a> Merge pull request <a href="">#1569</a> from jasongin/update-actions-cache-5.1.0</li>
<li><a href=""><code>30eb73b</code></a> Resolve high-severity audit issues</li>
<li><a href=""><code>4e1a87a</code></a> Update dist</li>
<li><a href=""><code>360237f</code></a> Strict equality</li>
<li><a href=""><code>4f8aac5</code></a> Bump <code>@​actions/cache</code> to 5.1.0, log cache write denied</li>
<li><a href=""><code>f4a67bb</code></a> Only use <code>mirrorToken</code> in <code>getManifest</code> if it's provided (<a href="">#1548</a>)</li>
<li><a href=""><code>0355742</code></a> Remove dummy NODE_AUTH_TOKEN export (<a href="">#1558</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/setup-node/compare/49933ea5288caeca8642d1e84afbd3f7d6820020...820762786026740c76f36085b0efc47a31fe5020">compare view</a></li>
</ul>
</details>
<br />

Updates `ossf/scorecard-action` from 2.4.3 to 2.4.4
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/ossf/scorecard-action/releases">ossf/scorecard-action's releases</a>.</em></p>
<blockquote>
<h2>v2.4.4</h2>
<h2>What's Changed</h2>
<p>This update bumps the Scorecard version to the v5.5.0 release. For a complete list of changes, please refer to the <a href="https://github.com/ossf/scorecard/releases/tag/v5.4.0">Scorecard v5.4.0 release notes</a> and the <a href="https://github.com/ossf/scorecard/releases/tag/v5.5.0">Scorecard v5.5.0 release notes</a>.</p>
<ul>
<li>log POST failures instead of failing entire action by <a href="https://github.com/spencerschrock"><code>@​spencerschrock</code></a> in <a href="">ossf/scorecard-action#1625</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/ossf/scorecard-action/compare/v2.4.3...v2.4.4">https://github.com/ossf/scorecard-action/compare/v2.4.3...v2.4.4</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2d11466</code></a> Bump action tag for v2.4.4 release (<a href="">#1688</a>)</li>
<li><a href=""><code>1bd3285</code></a> :seedling: Bump the docker-images group across 1 directory with 2 updates (<a href="">#1</a>...</li>
<li><a href=""><code>913edce</code></a> :seedling: Bump github.com/containerd/containerd from 1.7.32 to 1.7.33 (<a href="">#1671</a>)</li>
<li><a href=""><code>0957b8f</code></a> :seedling: Bump golang.org/x/net from 0.56.0 to 0.57.0 (<a href="">#1680</a>)</li>
<li><a href=""><code>f0061eb</code></a> :seedling: Bump google.golang.org/grpc from 1.81.1 to 1.82.1 (<a href="">#1687</a>)</li>
<li><a href=""><code>20ee732</code></a> :seedling: Bump github.com/sigstore/cosign/v2 from 2.6.3 to 2.6.4 (<a href="">#1685</a>)</li>
<li><a href=""><code>9f295ef</code></a> :seedling: Bump the github-actions group with 6 updates (<a href="">#1686</a>)</li>
<li><a href=""><code>69bf556</code></a> :seedling: Bump github.com/sigstore/sigstore-go from 1.1.4 to 1.2.0 (<a href="">#1681</a>)</li>
<li><a href=""><code>94e8b96</code></a> :seedling: Bump github.com/sigstore/rekor from 1.5.0 to 1.5.2 (<a href="">#1673</a>)</li>
<li><a href=""><code>c7a1b37</code></a> :seedling: Bump github.com/sigstore/fulcio from 1.8.5 to 1.8.6 (<a href="">#1675</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/ossf/scorecard-action/compare/4eaacf0543bb3f2c246792bd56e8cdeffafb205a...2d1146689b8cda280b9bc96326124645441f03bc">compare view</a></li>
</ul>
</details>
<br />

Updates `github/codeql-action/upload-sarif` from 4.37.0 to 4.37.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/github/codeql-action/releases">github/codeql-action/upload-sarif's releases</a>.</em></p>
<blockquote>
<h2>v4.37.3</h2>
<p>No user facing changes.</p>
<h2>v4.37.2</h2>
<ul>
<li>The new address format for the <code>config-file</code> input that was introduced in CodeQL Action 4.37.0 is now enabled by default. In addition to the format described there, the <code>remote=</code> prefix can now be used to explicitly indicate that the input refers to a remote file. All previous input formats continue to be accepted as well. <a href="">#4023</a></li>
<li>The CodeQL Action can now make use of <a href="https://docs.github.com/en/code-security/how-tos/secure-at-scale/configure-organization-security/manage-usage-and-access/giving-org-access-private-registries">configured private registries</a> in Default Setup to retrieve CodeQL configuration files from remote repositories that require authentication. This will allow customers to store their CodeQL configuration in a single repository that can then be referenced by Default Setup workflows in other repositories. We expect to roll this and other, related changes out to everyone in July. <a href="">#4007</a></li>
</ul>
<h2>v4.37.1</h2>
<ul>
<li><em>Upcoming breaking change</em>: Add a deprecation warning for customers using CodeQL version 2.20.6 and earlier. These versions of CodeQL were discontinued on 1 July 2026 alongside GitHub Enterprise Server 3.16, and will be unsupported by the next minor release of the CodeQL Action. <a href="">#3956</a></li>
<li>Update default CodeQL bundle version to <a href="https://github.com/github/codeql-action/releases/tag/codeql-bundle-v2.26.1">2.26.1</a>. <a href="">#4019</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/github/codeql-action/blob/main/CHANGELOG.md">github/codeql-action/upload-sarif's changelog</a>.</em></p>
<blockquote>
<h1>CodeQL Action Changelog</h1>
<p>See the <a href="https://github.com/github/codeql-action/releases">releases page</a> for the relevant changes to the CodeQL CLI and language packs.</p>
<h2>[UNRELEASED]</h2>
<ul>
<li>This version of the CodeQL Action adds support for the <code>tools</code> input for the <code>codeql-action/init</code> step to be specified using a <code>github-codeql-tools</code> <a href="https://docs.github.com/en/organizations/managing-organization-settings/managing-custom-properties-for-repositories-in-your-organization">repository property</a>. This feature will gradually be rolled out following the release of this version. Once rolled out, this allows for the CodeQL CLI version that is used in GitHub-managed workflows, such as Default Setup, to be set to a custom value. For example, customers who run into issues with rate limits when a new CodeQL CLI version is released can set the value to <code>toolcache</code> to always use the CodeQL CLI version that is available in the runner toolcache. For Advanced Setup workflows, the value provided for <code>tools</code> in the workflow definition always takes precedence unless the value of the repository property starts with <code>!</code>. <a href="">#4037</a></li>
<li>Update default CodeQL bundle version to <a href="https://github.com/github/codeql-action/releases/tag/codeql-bundle-v2.26.2">2.26.2</a>. <a href="">#4051</a></li>
</ul>
<h2>4.37.3 - 22 Jul 2026</h2>
<p>No user facing changes.</p>
<h2>4.37.2 - 21 Jul 2026</h2>
<ul>
<li>The new address format for the <code>config-file</code> input that was introduced in CodeQL Action 4.37.0 is now enabled by default. In addition to the format described there, the <code>remote=</code> prefix can now be used to explicitly indicate that the input refers to a remote file. All previous input formats continue to be accepted as well. <a href="">#4023</a></li>
<li>The CodeQL Action can now make use of <a href="https://docs.github.com/en/code-security/how-tos/secure-at-scale/configure-organization-security/manage-usage-and-access/giving-org-access-private-registries">configured private registries</a> in Default Setup to retrieve CodeQL configuration files from remote repositories that require authentication. This will allow customers to store their CodeQL configuration in a single repository that can then be referenced by Default Setup workflows in other repositories. We expect to roll this and other, related changes out to everyone in July. <a href="">#4007</a></li>
</ul>
<h2>4.37.1 - 16 Jul 2026</h2>
<ul>
<li><em>Upcoming breaking change</em>: Add a deprecation warning for customers using CodeQL version 2.20.6 and earlier. These versions of CodeQL were discontinued on 1 July 2026 alongside GitHub Enterprise Server 3.16, and will be unsupported by the next minor release of the CodeQL Action. <a href="">#3956</a></li>
<li>Update default CodeQL bundle version to <a href="https://github.com/github/codeql-action/releases/tag/codeql-bundle-v2.26.1">2.26.1</a>. <a href="">#4019</a></li>
</ul>
<h2>4.37.0 - 08 Jul 2026</h2>
<ul>
<li>Update default CodeQL bundle version to <a href="https://github.com/github/codeql-action/releases/tag/codeql-bundle-v2.26.0">2.26.0</a>. <a href="">#3995</a></li>
<li>In addition to the existing input format, the <code>config-file</code> input for the <code>codeql-action/init</code> step will soon support a new <code>[owner/]repo[@ref][:path]</code> format. All components except the repository name are optional. If omitted, <code>owner</code> defaults to the same owner as the repository the analysis is running for, <code>ref</code> to <code>main</code>, and <code>path</code> to <code>.github/codeql-action.yaml</code>. Support for this format ships in this version of the CodeQL Action, but will only be enabled over the coming weeks. <a href="">#3973</a></li>
</ul>
<h2>4.36.3 - 01 Jul 2026</h2>
<p>No user facing changes.</p>
<h2>4.36.2 - 04 Jun 2026</h2>
<ul>
<li>Cache CodeQL CLI version information across Actions steps. <a href="">#3943</a></li>
<li>Reduce requests while waiting for analysis processing by using exponential backoff when polling SARIF processing status. <a href="">#3937</a></li>
<li>Update default CodeQL bundle version to <a href="https://github.com/github/codeql-action/releases/tag/codeql-bundle-v2.25.6">2.25.6</a>. <a href="">#3948</a></li>
</ul>
<h2>4.36.1 - 02 Jun 2026</h2>
<p>No user facing changes.</p>
<h2>4.36.0 - 22 May 2026</h2>
<ul>
<li><em>Breaking change</em>: Bump the minimum required CodeQL bundle version to 2.19.4. <a href="">#3894</a></li>
<li>Add support for SHA-256 Git object IDs. <a href="">#3893</a></li>
<li>Update default CodeQL bundle version to <a href="https://github.com/github/codeql-action/releases/tag/codeql-bundle-v2.25.5">2.25.5</a>. <a href="">#3926</a></li>
</ul>
<h2>4.35.5 - 15 May 2026</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>e4fba86</code></a> Merge pull request <a href="">#4031</a> from github/update-v4.37.3-72f6a9da0</li>
<li><a href=""><code>fb50ab5</code></a> Update changelog for v4.37.3</li>
<li><a href=""><code>72f6a9d</code></a> Merge pull request <a href="">#4030</a> from github/mbg/fix/no-proxy</li>
<li><a href=""><code>3b5ee58</code></a> Use default <code>request</code> options instead of <code>undefined</code></li>
<li><a href=""><code>bfb6be4</code></a> Merge pull request <a href="">#4028</a> from github/mergeback/v4.37.2-to-main-e0647621</li>
<li><a href=""><code>526ab84</code></a> Rebuild</li>
<li><a href=""><code>d6217b9</code></a> Update changelog and version after v4.37.2</li>
<li><a href=""><code>e064762</code></a> Merge pull request <a href="">#4027</a> from github/update-v4.37.2-385bcdc5a</li>
<li><a href=""><code>e0faed8</code></a> Add a couple of change notes</li>
<li><a href=""><code>73aad0e</code></a> Update changelog for v4.37.2</li>
<li>Additional commits viewable in <a href="https://github.com/github/codeql-action/compare/99df26d4f13ea111d4ec1a7dddef6063f76b97e9...e4fba868fa4b1b91e1fdab776edc8cfbe6e9fb81">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2d8adb107b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.