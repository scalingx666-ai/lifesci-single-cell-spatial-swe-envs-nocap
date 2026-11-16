# Issue

**Title:** chore(deps): bump the actions-deps group across 1 directory with 8 updates

## Description

Bumps the actions-deps group with 8 updates in the / directory:

| Package | From | To |
| --- | --- | --- |
| [actions/checkout](https://github.com/actions/checkout) | `7.0.0` | `7.0.1` |
| [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv) | `8.3.2` | `10.1.0` |
| [pypa/gh-action-pypi-publish](https://github.com/pypa/gh-action-pypi-publish) | `1.14.0` | `1.14.2` |
| [actions/cache](https://github.com/actions/cache) | `4.3.0` | `6.1.0` |
| [actions/setup-python](https://github.com/actions/setup-python) | `6.3.0` | `7.0.0` |
| [actions/upload-artifact](https://github.com/actions/upload-artifact) | `4.6.2` | `7.0.1` |
| [codecov/codecov-action](https://github.com/codecov/codecov-action) | `7.0.0` | `7.1.0` |
| [re-actors/alls-green](https://github.com/re-actors/alls-green) | `1.2.2` | `1.3.0` |

Updates `actions/checkout` from 7.0.0 to 7.0.1
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
</blockquote>
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
<li>Additional commits viewable in <a href="https://github.com/actions/checkout/compare/9c091bb21b7c1c1d1991bb908d89e4e9dddfe3e0...3d3c42e5aac5ba805825da76410c181273ba90b1">compare view</a></li>
</ul>
</details>
<br />

Updates `astral-sh/setup-uv` from 8.3.2 to 10.1.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/setup-uv/releases">astral-sh/setup-uv's releases</a>.</em></p>
<blockquote>
<h2>v10.1.0 🌈  New output <code>python-runtime-id</code>and respect NO_PROXY</h2>
<h2>Changes</h2>
<p>This release adds more bheind the scene security improvements and also 2 small improvements.</p>
<h3>NO_PROXY</h3>
<p>This action now respects <code>no_proxy/NO_PROXY</code> environment variables which were previously ignored.</p>
<h3>New output <code>python-runtime-id</code></h3>
<p>The new output <code>python-runtime-id</code> can be used to know which python version exactly was installed if you use <code>activate-environment</code>. See <a href="">pyca/cryptography#15572</a> for details on why this can be useful.</p>
<h2>🐛 Bug fixes</h2>
<ul>
<li>fix: respect no proxy directive <a href="https://github.com/mj0nez"><code>@​mj0nez</code></a> (<a href="">#1037</a>)</li>
<li>Use JSON + a typed wrapper instead of TS codegen <a href="https://github.com/woodruffw"><code>@​woodruffw</code></a> (<a href="">#1025</a>)</li>
</ul>
<h2>🚀 Enhancements</h2>
<ul>
<li>Expose a Python &quot;identity&quot; output <a href="https://github.com/woodruffw"><code>@​woodruffw</code></a> (<a href="">#1036</a>)</li>
<li>Verify downloads with astral-sh/versions checksums <a href="https://github.com/zaniebot"><code>@​zaniebot</code></a> (<a href="">#1033</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.12.12 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1041</a>)</li>
<li>chore: update known checksums for 0.12.10/0.12.11 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1038</a>)</li>
<li>chore: update known checksums for 0.12.9 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1035</a>)</li>
<li>chore: update known checksums for 0.12.7/0.12.8 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1031</a>)</li>
<li>chore: update known checksums for 0.12.6 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1030</a>)</li>
<li>chore: update known checksums for 0.12.5 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1020</a>)</li>
<li>Use self-repo syntax for all in-repo actions/reusable workflows <a href="https://github.com/woodruffw"><code>@​woodruffw</code></a> (<a href="">#1024</a>)</li>
<li>Pin one-shot tools <a href="https://github.com/woodruffw"><code>@​woodruffw</code></a> (<a href="">#1022</a>)</li>
<li>ci: remove obsolete direct push attempts <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#1019</a>)</li>
</ul>
<h2>📚 Documentation</h2>
<ul>
<li>docs: update version references to v10.0.1 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1018</a>)</li>
</ul>
<h2>⬆️ Dependency updates</h2>
<ul>
<li>chore(deps-dev): roll up Dependabot updates <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#1043</a>)</li>
<li>Harden npm install defaults <a href="https://github.com/zaniebot"><code>@​zaniebot</code></a> (<a href="">#1026</a>)</li>
<li>Add dependency cooldowns <a href="https://github.com/woodruffw"><code>@​woodruffw</code></a> (<a href="">#1021</a>)</li>
</ul>
<h2>v10.0.1 🌈 Tolerate transient manifest timeouts</h2>
<h2>Changes</h2>
<p>Thank you <a href="https://github.com/arguile"><code>@​arguile</code></a>- for making this action more resilient.</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>bec219d</code></a> chore(deps-dev): roll up Dependabot updates (<a href="">#1043</a>)</li>
<li><a href=""><code>b90ec40</code></a> fix: respect no proxy directive (<a href="">#1037</a>)</li>
<li><a href=""><code>421feb6</code></a> chore: update known checksums for 0.12.12 (<a href="">#1041</a>)</li>
<li><a href=""><code>f634bf4</code></a> Expose a Python &quot;identity&quot; output (<a href="">#1036</a>)</li>
<li><a href=""><code>a6772c8</code></a> chore: update known checksums for 0.12.10/0.12.11 (<a href="">#1038</a>)</li>
<li><a href=""><code>e105c8f</code></a> chore: update known checksums for 0.12.9 (<a href="">#1035</a>)</li>
<li><a href=""><code>cd13f92</code></a> Verify downloads with astral-sh/versions checksums (<a href="">#1033</a>)</li>
<li><a href=""><code>3aef7b9</code></a> chore: update known checksums for 0.12.7/0.12.8 (<a href="">#1031</a>)</li>
<li><a href=""><code>d08d816</code></a> chore: update known checksums for 0.12.6 (<a href="">#1030</a>)</li>
<li><a href=""><code>19b4d1e</code></a> Harden npm install defaults (<a href="">#1026</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/setup-uv/compare/11f9893b081a58869d3b5fccaea48c9e9e46f990...bec219d24cd3e171d82865faccec33120bb574f4">compare view</a></li>
</ul>
</details>
<br />

Updates `pypa/gh-action-pypi-publish` from 1.14.0 to 1.14.2
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
<li><a href=""><code>ba38be9</code></a> Merge pull request <a href="">#408</a> from adisivaprasad/bump-setup-python-v6</li>
<li><a href=""><code>a6c5088</code></a> Bump actions/setup-python from v5.6.0 to v6.2.0</li>
<li>See full diff in <a href="https://github.com/pypa/gh-action-pypi-publish/compare/cef221092ed1bacb1cc03d23a2d87d1d172e277b...dc37677b2e1c63e2034f94d8a5b11f265b73ba33">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/cache` from 4.3.0 to 6.1.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/cache/releases">actions/cache's releases</a>.</em></p>
<blockquote>
<h2>v6.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Bump <code>@​actions/cache</code> to v6.1.0 - handle read-only cache access by <a href="https://github.com/jasongin"><code>@​jasongin</code></a> in <a href="">actions/cache#1768</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/cache/compare/v6...v6.1.0">https://github.com/actions/cache/compare/v6...v6.1.0</a></p>
<h2>v6.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update packages, migrate to ESM by <a href="https://github.com/Samirat"><code>@​Samirat</code></a> in <a href="">actions/cache#1760</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/cache/compare/v5...v6.0.0">https://github.com/actions/cache/compare/v5...v6.0.0</a></p>
<h2>v5.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Bump <code>@​actions/cache</code> to v5.1.0 - handle read-only cache access by <a href="https://github.com/jasongin"><code>@​jasongin</code></a> in <a href="">actions/cache#1775</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/cache/compare/v5...v5.1.0">https://github.com/actions/cache/compare/v5...v5.1.0</a></p>
<h2>v5.0.5</h2>
<h2>What's Changed</h2>
<ul>
<li>Update ts-http-runtime dependency by <a href="https://github.com/yacaovsnc"><code>@​yacaovsnc</code></a> in <a href="">actions/cache#1747</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/cache/compare/v5...v5.0.5">https://github.com/actions/cache/compare/v5...v5.0.5</a></p>
<h2>v5.0.4</h2>
<h2>What's Changed</h2>
<ul>
<li>Add release instructions and update maintainer docs by <a href="https://github.com/Link"><code>@​Link</code></a>- in <a href="">actions/cache#1696</a></li>
<li>Potential fix for code scanning alert no. 52: Workflow does not contain permissions by <a href="https://github.com/Link"><code>@​Link</code></a>- in <a href="">actions/cache#1697</a></li>
<li>Fix workflow permissions and cleanup workflow names / formatting by <a href="https://github.com/Link"><code>@​Link</code></a>- in <a href="">actions/cache#1699</a></li>
<li>docs: Update examples to use the latest version by <a href="https://github.com/XZTDean"><code>@​XZTDean</code></a> in <a href="">actions/cache#1690</a></li>
<li>Fix proxy integration tests by <a href="https://github.com/Link"><code>@​Link</code></a>- in <a href="">actions/cache#1701</a></li>
<li>Fix cache key in examples.md for bun.lock by <a href="https://github.com/RyPeck"><code>@​RyPeck</code></a> in <a href="">actions/cache#1722</a></li>
<li>Update dependencies &amp; patch security vulnerabilities by <a href="https://github.com/Link"><code>@​Link</code></a>- in <a href="">actions/cache#1738</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/XZTDean"><code>@​XZTDean</code></a> made their first contribution in <a href="">actions/cache#1690</a></li>
<li><a href="https://github.com/RyPeck"><code>@​RyPeck</code></a> made their first contribution in <a href="">actions/cache#1722</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/cache/compare/v5...v5.0.4">https://github.com/actions/cache/compare/v5...v5.0.4</a></p>
<h2>v5.0.3</h2>
<h2>What's Changed</h2>
<ul>
<li>Bump <code>@actions/cache</code> to v5.0.5 (Resolves: <a href="https://github.com/actions/cache/security/dependabot/33">https://github.com/actions/cache/security/dependabot/33</a>)</li>
<li>Bump <code>@actions/core</code> to v2.0.3</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/cache/blob/main/RELEASES.md">actions/cache's changelog</a>.</em></p>
<blockquote>
<h1>Releases</h1>
<h2>How to prepare a release</h2>
<blockquote>
<p>[!NOTE]
Relevant for maintainers with write access only.</p>
</blockquote>
<ol>
<li>Switch to a new branch from <code>main</code>.</li>
<li>Run <code>npm test</code> to ensure all tests are passing.</li>
<li>Update the version in <a href="https://github.com/actions/cache/blob/main/package.json"><code>https://github.com/actions/cache/blob/main/package.json</code></a>.</li>
<li>Run <code>npm run build</code> to update the compiled files.</li>
<li>Update this <a href="https://github.com/actions/cache/blob/main/RELEASES.md"><code>https://github.com/actions/cache/blob/main/RELEASES.md</code></a> with the new version and changes in the <code>## Changelog</code> section.</li>
<li>Run <code>licensed cache</code> to update the license report.</li>
<li>Run <code>licensed status</code> and resolve any warnings by updating the <a href="https://github.com/actions/cache/blob/main/.licensed.yml"><code>https://github.com/actions/cache/blob/main/.licensed.yml</code></a> file with the exceptions.</li>
<li>Commit your changes and push your branch upstream.</li>
<li>Open a pull request against <code>main</code> and get it reviewed and merged.</li>
<li>Draft a new release <a href="https://github.com/actions/cache/releases">https://github.com/actions/cache/releases</a> use the same version number used in <code>package.json</code>
<ol>
<li>Create a new tag with the version number.</li>
<li>Auto generate release notes and update them to match the changes you made in <code>RELEASES.md</code>.</li>
<li>Toggle the set as the latest release option.</li>
<li>Publish the release.</li>
</ol>
</li>
<li>Navigate to <a href="https://github.com/actions/cache/actions/workflows/release-new-action-version.yml">https://github.com/actions/cache/actions/workflows/release-new-action-version.yml</a>
<ol>
<li>There should be a workflow run queued with the same version number.</li>
<li>Approve the run to publish the new version and update the major tags for this action.</li>
</ol>
</li>
</ol>
<h2>Changelog</h2>
<h3>6.1.0</h3>
<ul>
<li>Bump <code>@actions/cache</code> to v6.1.0 to pick up <a href="">actions/toolkit#2435 Handle cache write error due to read-only token</a></li>
<li>Switch redundant &quot;Cache save failed&quot; warning to debug log in save-only</li>
</ul>
<h3>6.0.0</h3>
<ul>
<li>Updated <code>@actions/cache</code> to ^6.0.1, <code>@actions/core</code> to ^3.0.1, <code>@actions/exec</code> to ^3.0.0, <code>@actions/io</code> to ^3.0.2</li>
<li>Migrated to ESM module system</li>
<li>Upgraded Jest to v30 and test infrastructure to be ESM compatible</li>
</ul>
<h3>5.0.4</h3>
<ul>
<li>Bump <code>minimatch</code> to v3.1.5 (fixes ReDoS via globstar patterns)</li>
<li>Bump <code>undici</code> to v6.24.1 (WebSocket decompression bomb protection, header validation fixes)</li>
<li>Bump <code>fast-xml-parser</code> to v5.5.6</li>
</ul>
<h3>5.0.3</h3>
<ul>
<li>Bump <code>@actions/cache</code> to v5.0.5 (Resolves: <a href="https://github.com/actions/cache/security/dependabot/33">https://github.com/actions/cache/security/dependabot/33</a>)</li>
<li>Bump <code>@actions/core</code> to v2.0.3</li>
</ul>
<h3>5.0.2</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>55cc834</code></a> Merge pull request <a href="">#1768</a> from jasongin/readonly-cache</li>
<li><a href=""><code>d8cd72f</code></a> Bump <code>@​actions/cache</code> to v6.1.0 - handle cache write error due to RO token</li>
<li><a href=""><code>2c8a9bd</code></a> Merge pull request <a href="">#1760</a> from actions/samirat/esm_migration_and_package_update</li>
<li><a href=""><code>e9b91fd</code></a> Prettier fixes</li>
<li><a href=""><code>e4884b8</code></a> Rebuild dist</li>
<li><a href=""><code>10baf01</code></a> Fixed licenses</li>
<li><a href=""><code>e39b386</code></a> Fix test mock return order</li>
<li><a href=""><code>b692820</code></a> PR feedback</li>
<li><a href=""><code>6074912</code></a> Rebuild dist bundles as ESM to match type:module</li>
<li><a href=""><code>5a912e8</code></a> Fix lint and jest issues</li>
<li>Additional commits viewable in <a href="https://github.com/actions/cache/compare/0057852bfaa89a56745cba8c7296529d2fc39830...55cc8345863c7cc4c66a329aec7e433d2d1c52a9">compare view</a></li>
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

Updates `actions/upload-artifact` from 4.6.2 to 7.0.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/upload-artifact/releases">actions/upload-artifact's releases</a>.</em></p>
<blockquote>
<h2>v7.0.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Update the readme with direct upload details by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/upload-artifact#795</a></li>
<li>Readme: bump all the example versions to v7 by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/upload-artifact#796</a></li>
<li>Include changes in typespec/ts-http-runtime 0.3.5 by <a href="https://github.com/yacaovsnc"><code>@​yacaovsnc</code></a> in <a href="">actions/upload-artifact#797</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/upload-artifact/compare/v7...v7.0.1">https://github.com/actions/upload-artifact/compare/v7...v7.0.1</a></p>
<h2>v7.0.0</h2>
<h2>v7 What's new</h2>
<h3>Direct Uploads</h3>
<p>Adds support for uploading single files directly (unzipped). Callers can set the new <code>archive</code> parameter to <code>false</code> to skip zipping the file during upload. Right now, we only support single files. The action will fail if the glob passed resolves to multiple files. The <code>name</code> parameter is also ignored with this setting. Instead, the name of the artifact will be the name of the uploaded file.</p>
<h3>ESM</h3>
<p>To support new versions of the <code>@actions/*</code> packages, we've upgraded the package to ESM.</p>
<h2>What's Changed</h2>
<ul>
<li>Add proxy integration test by <a href="https://github.com/Link"><code>@​Link</code></a>- in <a href="">actions/upload-artifact#754</a></li>
<li>Upgrade the module to ESM and bump dependencies by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/upload-artifact#762</a></li>
<li>Support direct file uploads by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/upload-artifact#764</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/Link"><code>@​Link</code></a>- made their first contribution in <a href="">actions/upload-artifact#754</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/upload-artifact/compare/v6...v7.0.0">https://github.com/actions/upload-artifact/compare/v6...v7.0.0</a></p>
<h2>v6.0.0</h2>
<h2>v6 - What's new</h2>
<blockquote>
<p>[!IMPORTANT]
actions/upload-artifact@v6 now runs on Node.js 24 (<code>runs.using: node24</code>) and requires a minimum Actions Runner version of 2.327.1. If you are using self-hosted runners, ensure they are updated before upgrading.</p>
</blockquote>
<h3>Node.js 24</h3>
<p>This release updates the runtime to Node.js 24. v5 had preliminary support for Node.js 24, however this action was by default still running on Node.js 20. Now this action by default will run on Node.js 24.</p>
<h2>What's Changed</h2>
<ul>
<li>Upload Artifact Node 24 support by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/upload-artifact#719</a></li>
<li>fix: update <code>@​actions/artifact</code> for Node.js 24 punycode deprecation by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/upload-artifact#744</a></li>
<li>prepare release v6.0.0 for Node.js 24 support by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/upload-artifact#745</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/upload-artifact/compare/v5.0.0...v6.0.0">https://github.com/actions/upload-artifact/compare/v5.0.0...v6.0.0</a></p>
<h2>v5.0.0</h2>
<h2>What's Changed</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>043fb46</code></a> Merge pull request <a href="">#797</a> from actions/yacaovsnc/update-dependency</li>
<li><a href=""><code>634250c</code></a> Include changes in typespec/ts-http-runtime 0.3.5</li>
<li><a href=""><code>e454baa</code></a> Readme: bump all the example versions to v7 (<a href="">#796</a>)</li>
<li><a href=""><code>74fad66</code></a> Update the readme with direct upload details (<a href="">#795</a>)</li>
<li><a href=""><code>bbbca2d</code></a> Support direct file uploads (<a href="">#764</a>)</li>
<li><a href=""><code>589182c</code></a> Upgrade the module to ESM and bump dependencies (<a href="">#762</a>)</li>
<li><a href=""><code>47309c9</code></a> Merge pull request <a href="">#754</a> from actions/Link-/add-proxy-integration-tests</li>
<li><a href=""><code>02a8460</code></a> Add proxy integration test</li>
<li><a href=""><code>b7c566a</code></a> Merge pull request <a href="">#745</a> from actions/upload-artifact-v6-release</li>
<li><a href=""><code>e516bc8</code></a> docs: correct description of Node.js 24 support in README</li>
<li>Additional commits viewable in <a href="https://github.com/actions/upload-artifact/compare/ea165f8d65b6e75b540449e92b4886f43607fa02...043fb46d1a93c77aae656e7c1c64a875d1fc6a0a">compare view</a></li>
</ul>
</details>
<br />

Updates `codecov/codecov-action` from 7.0.0 to 7.1.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/releases">codecov/codecov-action's releases</a>.</em></p>
<blockquote>
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
<li><a href=""><code>0b35c9e</code></a> chore(release): 7.1.0 (<a href="">#1971</a>)</li>
<li>See full diff in <a href="https://github.com/codecov/codecov-action/compare/fb8b3582c8e4def4969c97caa2f19720cb33a72f...0b35c9ecc4f0529d0eb674914510c22f85b196b4">compare view</a></li>
</ul>
</details>
<br />

Updates `re-actors/alls-green` from 1.2.2 to 1.3.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/re-actors/alls-green/releases">re-actors/alls-green's releases</a>.</em></p>
<blockquote>
<h2>v1.3.0</h2>
<!-- raw HTML omitted -->
<h2>🛡️ What's Unmessed</h2>
<blockquote>
<p>[!caution]</p>
<p>There was a small command injection risk in prior versions. I consider it very low because of the specifics of the action use case. But still, do upgrade, okay?</p>
<p><a href="https://github.com/illera88"><code>@​illera88</code></a><a href="https://github.com/sponsors/max-sixty">💰</a> fixed this <a href="https://docs.zizmor.sh/audits/#template-injection">template injection</a> bug in <a href="">#37</a> by passing inputs via env vars.</p>
<p>See GHSA-gj76-h2ch-5m76 for more detail that was first reported by <a href="https://github.com/Corbynx010"><code>@​Corbynx010</code></a><a href="https://github.com/sponsors/Corbynx010">💰</a> while I was at EuroPython.</p>
</blockquote>
<h2>✨ What's Improved</h2>
<p>I did a bunch of internal refactoring including hints of what <a href="https://github.com/max-sixty"><code>@​max-sixty</code></a><a href="https://github.com/sponsors/max-sixty">💰</a> reported in <a href="">#23</a>. And took a small patch of <a href="https://github.com/krokofant"><code>@​krokofant</code></a><a href="https://github.com/sponsors/krokofant">💰</a> in. This involved a bunch of preparatory infra work with testing infra.</p>
<p>One notable improvement is that now thanks to <a href="https://github.com/tomasr8"><code>@​tomasr8</code></a><a href="https://github.com/sponsors/tomasr8">💰</a>'s and <a href="https://github.com/hugovk"><code>@​hugovk</code></a><a href="https://github.com/sponsors/hugovk">💰</a>'s UX suggestions in <a href="">#31</a>, the gate status output is colored in the console and should be easier to scan in the log output per line. They entries now have leading <code>✓</code>/<code>❌</code> acceptance marks and the actual incoming job outcomes are labeled with <code>🟢</code>/<code>🔴</code>/<code>⬜</code>/<code>⚫</code>.</p>
<h2>🐛 What's Fixed</h2>
<p>The job-statuses summary could print &quot;Some of the allowed to be skipped jobs did not succeed&quot; based on the wrong condition — it's now tied to <code>allowed-skips</code> as intended, not <code>allowed-failures</code>.</p>
<h2>💪 New Contributors</h2>
<ul>
<li><a href="https://github.com/Corbynx010"><code>@​Corbynx010</code></a><a href="https://github.com/sponsors/Corbynx010">💰</a> lurked in GHSA-gj76-h2ch-5m76 before everyone else :wink:</li>
<li><a href="https://github.com/illera88"><code>@​illera88</code></a> made their first contribution in <a href="">#37</a> and GHSA-gj76-h2ch-5m76</li>
<li><a href="https://github.com/krokofant"><code>@​krokofant</code></a> and <a href="https://github.com/max-sixty"><code>@​max-sixty</code></a> first contributed in <a href="">#23</a></li>
<li><a href="https://github.com/tomasr8"><code>@​tomasr8</code></a> and <a href="https://github.com/hugovk"><code>@​hugovk</code></a> in <a href="">#31</a></li>
</ul>
<p><strong>🪞 Full Diff</strong>: <a href="https://github.com/re-actors/alls-green/compare/v1.2.2...v1.3.0">https://github.com/re-actors/alls-green/compare/v1.2.2...v1.3.0</a></p>
<p><strong>🧔‍♂️ Release Manager:</strong> <a href="https://github.com/sponsors/webknjaz"><code>@​webknjaz</code></a> <a href="https://stand-with-ukraine.pp.ua">🇺🇦</a></p>
<p><strong>💬 Discuss</strong> <a href="https://bsky.app/profile/did:plc:ve6s3mxkefjaxty3m4fdqumn/post/3mtn27ckwcs2g">on Bluesky 🦋</a>, <a href="https://mastodon.social/@webknjaz/117136385624434132">on Mastodon 🐘</a> and <a href="https://github.com/re-actors/alls-green/discussions/41">on GitHub</a>.</p>
<p><a href="https://github.com/sponsors/webknjaz"><img src="https://img.shields.io/badge/%40webknjaz-transparent?logo=githubsponsors&amp;logoColor=%23EA4AAA&amp;label=Sponsor&amp;color=2a313c" alt="GH Sponsors badge" /></a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b5b5b37</code></a> Merge pull request <a href="">#38</a> from re-actors/pre-commit-ci-update-config</li>
<li><a href=""><code>bd6edd6</code></a> [pre-commit.ci] pre-commit autoupdate</li>
<li><a href=""><code>3967c81</code></a> 💅 Make the output easier to scan</li>
<li><a href=""><code>e68df08</code></a> 💅 Style job statuses title with a 🔮</li>
<li><a href=""><code>62d37b2</code></a> 🧪 Unxfail 'success-of-some-allowed-to-skip-or-fail'</li>
<li><a href=""><code>7b5df6d</code></a> 💅 Add a Codecov badge to README</li>
<li><a href=""><code>2410c4c</code></a> 🐛 Correct reporting failed skipped jobs</li>
<li><a href=""><code>6457593</code></a> 💅 Add a GH Sponsors badge</li>
<li><a href=""><code>a617895</code></a> 💅 Add a pre-commit.ci badge</li>
<li><a href=""><code>8de05dc</code></a> 🧪 Force <code>ctrace</code> core in coveragepy</li>
<li>Additional commits viewable in <a href="https://github.com/re-actors/alls-green/compare/05ac9388f0aebcb5727afa17fcccfecd6f8ec5fe...b5b5b37504aa4183270bd3d855c52a67f212be35">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `775541662ed0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.