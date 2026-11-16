# Issue

**Title:** Bump the actions-deps group with 5 updates

## Description

Bumps the actions-deps group with 5 updates:

| Package | From | To |
| --- | --- | --- |
| [actions/checkout](https://github.com/actions/checkout) | `5.1.0` | `7.0.1` |
| [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv) | `8.1.0` | `10.3.0` |
| [actions/setup-python](https://github.com/actions/setup-python) | `6.3.0` | `7.0.0` |
| [pypa/cibuildwheel](https://github.com/pypa/cibuildwheel) | `3.4.1` | `4.3.2` |
| [codecov/codecov-action](https://github.com/codecov/codecov-action) | `7.0.0` | `7.1.1` |

Updates `actions/checkout` from 5.1.0 to 7.0.1
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
<li>Additional commits viewable in <a href="https://github.com/actions/checkout/compare/v5.1.0...3d3c42e5aac5ba805825da76410c181273ba90b1">compare view</a></li>
</ul>
</details>
<br />

Updates `astral-sh/setup-uv` from 8.1.0 to 10.3.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/setup-uv/releases">astral-sh/setup-uv's releases</a>.</em></p>
<blockquote>
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
<h2>⬆️ Dependency updates</h2>
<ul>
<li>chore(deps): bump zizmorcore/zizmor-action from 0.6.2 to 0.6.3 @<a href="https://github.com/apps/dependabot">dependabot[bot]</a> (<a href="">#1077</a>)</li>
</ul>
<h2>v10.2.0 🌈 Disable automatic cache saves for merge queues</h2>
<h2>Changes</h2>
<p>This release contains the known-checksum of the most recent uv releases and also disabled the uploading(saving) of the cache when in a merge queue since theses caches would almost never be used.</p>
<h2>🚀 Enhancements</h2>
<ul>
<li>Disable automatic cache saves for merge queues <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#1056</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.12.17 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1058</a>)</li>
<li>chore: update known checksums for 0.12.16 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1057</a>)</li>
<li>chore: update known checksums for 0.12.15 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1054</a>)</li>
<li>chore: update known checksums for 0.12.14 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1053</a>)</li>
<li>chore: update known checksums for 0.12.13 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1045</a>)</li>
</ul>
<h2>📚 Documentation</h2>
<ul>
<li>docs: update version references to v10.1.0 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1044</a>)</li>
</ul>
<h2>⬆️ Dependency updates</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1c37ad0</code></a> chore: update known checksums for 0.13.0 (<a href="">#1089</a>)</li>
<li><a href=""><code>b3c9b5f</code></a> chore: update known checksums for 0.12.24 (<a href="">#1084</a>)</li>
<li><a href=""><code>b06acff</code></a> Add <code>python-arch</code> support (<a href="">#1079</a>)</li>
<li><a href=""><code>c84232c</code></a> chore: update known checksums for 0.12.23 (<a href="">#1082</a>)</li>
<li><a href=""><code>51fdd26</code></a> Use macOS 15 runners for tests (<a href="">#1081</a>)</li>
<li><a href=""><code>a96208b</code></a> chore: update known checksums for 0.12.22 (<a href="">#1080</a>)</li>
<li><a href=""><code>0e3884b</code></a> chore: update known checksums for 0.12.21 (<a href="">#1078</a>)</li>
<li><a href=""><code>bcf0580</code></a> chore: update known checksums for 0.12.20 (<a href="">#1076</a>)</li>
<li><a href=""><code>b92a892</code></a> chore(deps): bump zizmorcore/zizmor-action from 0.6.2 to 0.6.3 (<a href="">#1077</a>)</li>
<li><a href=""><code>227a0f6</code></a> chore: update known checksums for 0.12.19 (<a href="">#1068</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/setup-uv/compare/v8.1.0...1c37ad07a6a961277cf70c0d37d6f313000f5884">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/setup-python` from 6.3.0 to 7.0.0
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
</blockquote>
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
<li>See full diff in <a href="https://github.com/actions/setup-python/compare/ece7cb06caefa5fff74198d8649806c4678c61a1...5fda3b95a4ea91299a34e894583c3862153e4b97">compare view</a></li>
</ul>
</details>
<br />

Updates `pypa/cibuildwheel` from 3.4.1 to 4.3.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pypa/cibuildwheel/releases">pypa/cibuildwheel's releases</a>.</em></p>
<blockquote>
<h2>v4.3.2</h2>
<ul>
<li>🔐 Updates our dependency pins to certifi==2026.10.19, following the <a href="https://emudhra.we-have-a-problem.com/">eMudhra Intermediate CA Compromise</a>. Linux builds may still be vulnerable through manylinux images - a patch release will soon follow if so.</li>
</ul>
<h2>v4.3.1</h2>
<ul>
<li>🛠 Updates CPython 3.15 to the final 3.15.0 release (<a href="">#3009</a>)</li>
</ul>
<h2>v4.3.0</h2>
<ul>
<li>✨ Extends <a href="https://cibuildwheel.pypa.io/en/stable/configuration/#inherit">option inheritance</a> to every configuration layer, so global and platform-specific settings can append or prepend to existing values, including cibuildwheel's defaults. Environment variables can also extend earlier settings using <code>CIBW_INHERIT</code>. (<a href="">#2928</a>)</li>
<li>✨ Adds PyPy 3.12 support and updates PyPy 3.11 to v8.0.0, available with the <code>pypy</code> <a href="https://cibuildwheel.pypa.io/en/stable/options/#enable"><code>enable</code></a> flag (<a href="">#2998</a>)</li>
<li>✨ Adds GraalPy 3.13 (v25.3) support on Linux, Windows, and macOS arm64, available with the <code>graalpy</code> <a href="https://cibuildwheel.pypa.io/en/stable/options/#enable"><code>enable</code></a> flag (<a href="">#2982</a>)</li>
<li>✨ Adds <a href="https://cibuildwheel.pypa.io/en/stable/options/#log-fold-mode"><code>log-fold-mode</code></a> to override CI log folding, including <code>CIBW_LOG_FOLD_MODE=disabled</code> to keep build steps expanded (<a href="">#2972</a>)</li>
<li>✨ Adds a <code>python-path</code> input to the GitHub Action to choose the Python interpreter used to run cibuildwheel, and falls back to system <code>python3</code> on runner architectures unsupported by <code>setup-python</code>, such as native riscv64 (<a href="">#2990</a>)</li>
<li>🐛 Fixes Windows command execution when paths or arguments contain shell metacharacters, including dependency specifiers containing <code>&lt;</code> or <code>&gt;</code> (<a href="">#2978</a>)</li>
<li>🛠 Improves readability of logged commands whose arguments contain quotes (<a href="">#2993</a>)</li>
<li>🛠 Updates Pyodide to 0.27.8, 0.29.5, and 314.0.7, and updates its build tooling, including auditwheel-emscripten 0.3.0 (<a href="">#2996</a>)</li>
<li>🛠 Updates dependencies and container pins, including CPython 3.15.0rc3 (<a href="">#2986</a>, <a href="">#3003</a>)</li>
<li>📚 Corrects references to <code>--archs</code> in CLI help, error messages, and documentation (<a href="">#2992</a>)</li>
</ul>
<h2>v4.2.1</h2>
<ul>
<li>🐛 Respects the NuGet package sources configured on the machine when installing CPython on Windows, instead of always falling back to nuget.org (<a href="">#2966</a>)</li>
<li>🐛 Fixes a <code>NameError</code> on Pyodide when an already-compatible wheel was reused, which made the test step fail (<a href="">#2968</a>)</li>
<li>🛠 Updates the Android Python versions, and the Android testbed's Gradle version, making it compatible with Java 25 (<a href="">#2962</a>)</li>
<li>🛠 Updates dependencies including CPython 3.15.0rc2 (<a href="">#2965</a>, <a href="">#2970</a>, <a href="">#2976</a>, <a href="">#2981</a>, <a href="">#2985</a>)</li>
</ul>
<h2>v4.2.0</h2>
<ul>
<li>🌟 CPython 3.15 wheels are now built by default - without the <code>&quot;cpython-prerelease&quot;</code> <a href="https://cibuildwheel.pypa.io/en/stable/options/#enable"><code>enable</code></a> set. It's time to build and upload these wheels to PyPI! This release includes CPython 3.15.0rc1, which is guaranteed to be ABI compatible with the final release. (<a href="">#2944</a>)</li>
<li>✨ Adds Pyodide 3.15 support with the <code>cp315-pyodide_wasm32</code> build identifier, using Pyodide 315.0.0a2. These are also stable wrt. the final release. (<a href="">#2958</a>)</li>
<li>🐛 Retries a failed download six times with exponential backoff, so short network outages no longer stop a build. A <code>4xx</code> response is still reported at once. (<a href="">#2953</a>)</li>
<li>🐛 Accepts <code>default</code> as a <a href="https://cibuildwheel.pypa.io/en/stable/options/#build-frontend"><code>build-frontend</code></a> value on Pyodide, and accepts <code>pyodide-build</code> in the top-level table and in overrides (<a href="">#2951</a>)</li>
<li>🛠 Holds pip back on GraalPy, where newer pip breaks the build (<a href="">#2955</a>)</li>
<li>🛠 Updates Pyodide to 314.0.4 (<a href="">#2949</a>, <a href="">#2952</a>)</li>
<li>🛠 Updates dependencies and container pins (<a href="">#2952</a>, <a href="">#2960</a>)</li>
<li>💼 Updates CI action pins (<a href="">#2948</a>, <a href="">#2954</a>)</li>
<li>🧪 Uses pp311 for the abi3 test, and deletes <code>test_overridden_pip_constraint</code>, which is not necessary since <a href="">#2583</a> (<a href="">#2956</a>, <a href="">#2957</a>)</li>
</ul>
<h2>v4.1.1</h2>
<ul>
<li>✨ Adds <code>pyodide-build</code> as a separate <a href="https://cibuildwheel.pypa.io/en/stable/options/#build-frontend"><code>build-frontend</code></a>, now the default frontend for Pyodide, with verbosity flags handling. Any other frontend is ignored with a warning on Pyodide. (<a href="">#2609</a>, <a href="">#2945</a>)</li>
<li>🔐 Uses digests instead of tags for pinned container images, strengthening supply-chain security. The human-readable tags remain as comments in <code>pinned_docker_images.cfg</code>. (<a href="">#2915</a>)</li>
<li>🐛 Fixes platform-specific <a href="https://cibuildwheel.pypa.io/en/stable/options/#test-runtime"><code>test-runtime</code></a> environment variables (e.g. <code>CIBW_TEST_RUNTIME_ANDROID</code>) not being honored (<a href="">#2941</a>)</li>
<li>🐛 Fixes quoting of <a href="https://cibuildwheel.pypa.io/en/stable/options/#test-requires"><code>test-requires</code></a> and <a href="https://cibuildwheel.pypa.io/en/stable/options/#audit-requires"><code>audit-requires</code></a> so PEP 508 specifiers containing spaces work (<a href="">#2913</a>)</li>
<li>🐛 Makes <a href="https://cibuildwheel.pypa.io/en/stable/options/#archs"><code>archs</code></a> parsing case-insensitive and platform-aware, so e.g. <code>arm64</code> works on Windows (<a href="">#2920</a>)</li>
<li>🐛 Uses an absolute path for the <code>{project}</code> placeholder in <a href="https://cibuildwheel.pypa.io/en/stable/options/#config-settings"><code>config-settings</code></a> (<a href="">#2934</a>)</li>
<li>🐛 Validates the <a href="https://cibuildwheel.pypa.io/en/stable/options/#pyodide-version"><code>pyodide-version</code></a> option against the build identifier with a clear error (<a href="">#2925</a>)</li>
<li>🐛 Fixes PyPy installs on macOS after PyPy switched its downloads from <code>.tar.bz2</code> to <code>.tar.gz</code> (<a href="">#2939</a>)</li>
<li>🐛 Makes a matching <code>python3-config</code> available in the build and test venvs on macOS (<a href="">#2922</a>)</li>
<li>🛠 Updates dependencies and container pins (<a href="">#2917</a>, <a href="">#2935</a>, <a href="">#2939</a>)</li>
<li>🛠 Updates Android tests to current Python versions and the new test repository URL (<a href="">#2933</a>)</li>
<li>🛠 Drops the <code>orjson</code> dependency, no longer used by mypy 2+ (<a href="">#2923</a>)</li>
<li>📚 Builds the docs with properdocs, a MkDocs fork (<a href="">#2946</a>)</li>
<li>📚 Adds the missing <code>cp314-pyodide_wasm32</code> entry to the build identifier table (<a href="">#2947</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pypa/cibuildwheel/blob/main/docs/changelog.md">pypa/cibuildwheel's changelog</a>.</em></p>
<blockquote>
<hr />
<h2>title: Changelog
ref: changelog</h2>
<h1>Changelog</h1>
<h3>v4.3.4</h3>
<p><em>22 October 2026</em></p>
<ul>
<li>🔐 Warns when a uv build frontend is selected and the host uv is older than 0.13.4, which still trusts the compromised eMudhra CA roots (<a href="">#3021</a>)</li>
<li>🔐 Uses cibuildwheel's CA bundle for pip on Python 3.9, where pip uses its bundled certifi, which still trusts the compromised eMudhra roots (<a href="">#3017</a>)</li>
<li>🔐 Uses cibuildwheel's CA bundle for pip on GraalPy, where truststore is not supported (<a href="">#3019</a>)</li>
<li>🔐 Uses cibuildwheel's CA bundle in Android, iOS, and Pyodide cross venvs, where pip uses the host's OpenSSL CA file (<a href="">#3020</a>)</li>
<li>🐛 Seeds build's isolated environment with the pinned pip on macOS and Windows, fixing GraalPy 25.0 builds (<a href="">#3018</a>)</li>
<li>💼 Stops Azure cache growth from <code>restoreKeys</code> (<a href="">#3022</a>)</li>
</ul>
<h3>v4.3.3</h3>
<p><em>21 October 2026</em></p>
<ul>
<li>🔐 Updates manylinux images and pip to fix vulnerability to <a href="https://emudhra.we-have-a-problem.com/">eMudhra</a>.</li>
</ul>
<h3>v4.3.2</h3>
<p><em>20 October 2026</em></p>
<ul>
<li>🔐 Updates our dependency pins to certifi==2026.10.19, following the <a href="https://emudhra.we-have-a-problem.com/">eMudhra Intermediate CA Compromise</a>. Linux builds may still be vulnerable through manylinux images - a patch release will soon follow if so.</li>
</ul>
<h3>v4.3.1</h3>
<p><em>10 October 2026</em></p>
<ul>
<li>🛠 Updates CPython 3.15 to the final 3.15.0 release (<a href="">#3009</a>)</li>
</ul>
<h3>v4.3.0</h3>
<p><em>5 October 2026</em></p>
<ul>
<li>✨ Extends <a href="https://cibuildwheel.pypa.io/en/stable/configuration/#inherit">option inheritance</a> to every configuration layer, so global and platform-specific settings can append or prepend to existing values, including cibuildwheel's defaults. Environment variables can also extend earlier settings using <code>CIBW_INHERIT</code>. (<a href="">#2928</a>)</li>
<li>✨ Adds PyPy 3.12 support and updates PyPy 3.11 to v8.0.0, available with the <code>pypy</code> <a href="https://cibuildwheel.pypa.io/en/stable/options/#enable"><code>enable</code></a> flag (<a href="">#2998</a>)</li>
<li>✨ Adds GraalPy 3.13 (v25.3) support on Linux, Windows, and macOS arm64, available with the <code>graalpy</code> <a href="https://cibuildwheel.pypa.io/en/stable/options/#enable"><code>enable</code></a> flag (<a href="">#2982</a>)</li>
<li>✨ Adds <a href="https://cibuildwheel.pypa.io/en/stable/options/#log-fold-mode"><code>log-fold-mode</code></a> to override CI log folding, including <code>CIBW_LOG_FOLD_MODE=disabled</code> to keep build steps expanded (<a href="">#2972</a>)</li>
<li>✨ Adds a <code>python-path</code> input to the GitHub Action to choose the Python interpreter used to run cibuildwheel, and falls back to system <code>python3</code> on runner architectures unsupported by <code>setup-python</code>, such as native riscv64 (<a href="">#2990</a>)</li>
<li>🐛 Fixes Windows command execution when paths or arguments contain shell metacharacters, including dependency specifiers containing <code>&lt;</code> or <code>&gt;</code> (<a href="">#2978</a>)</li>
<li>🛠 Improves readability of logged commands whose arguments contain quotes (<a href="">#2993</a>)</li>
<li>🛠 Updates Pyodide to 0.27.8, 0.29.5, and 314.0.7, and updates its build tooling, including auditwheel-emscripten 0.3.0 (<a href="">#2996</a>)</li>
<li>🛠 Updates dependencies and container pins, including CPython 3.15.0rc3 (<a href="">#2986</a>, <a href="">#3003</a>)</li>
<li>📚 Corrects references to <code>--archs</code> in CLI help, error messages, and documentation (<a href="">#2992</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>f111813</code></a> Bump version: v4.3.2</li>
<li><a href=""><code>d5d8026</code></a> Bump certifi to 2026.10.19 (<a href="">#3015</a>)</li>
<li><a href=""><code>b3395e2</code></a> Bump version: v4.3.1</li>
<li><a href=""><code>5dbcbbb</code></a> [Bot] Update dependencies (<a href="">#3009</a>)</li>
<li><a href=""><code>2ea220c</code></a> chore: update flake8-lazy to v0.10.1 (<a href="">#3007</a>)</li>
<li><a href=""><code>e0d0953</code></a> [pre-commit.ci] pre-commit autoupdate (<a href="">#3006</a>)</li>
<li><a href=""><code>1362429</code></a> [Bot] Update dependencies (<a href="">#3005</a>)</li>
<li><a href=""><code>adba99c</code></a> Bump version: v4.3.0</li>
<li><a href=""><code>8a0d481</code></a> Add the ability to set 'inherit' at all levels of the options cascade (<a href="">#2928</a>)</li>
<li><a href=""><code>8bc038b</code></a> chore(deps): bump astral-sh/setup-uv from 10.1.0 to 10.2.0 in the actions gro...</li>
<li>Additional commits viewable in <a href="https://github.com/pypa/cibuildwheel/compare/8d2b08b68458a16aeb24b64e68a09ab1c8e82084...f11181315571b24e4a3c67f1a828532793f2df55">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `657351edd0c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.