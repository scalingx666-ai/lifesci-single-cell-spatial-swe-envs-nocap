# Issue

**Title:** Bump the actions-deps group with 5 updates

## Description

Bumps the actions-deps group with 5 updates:

| Package | From | To |
| --- | --- | --- |
| [actions/checkout](https://github.com/actions/checkout) | `7.0.0` | `7.0.1` |
| [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv) | `8.3.2` | `10.3.0` |
| [pypa/gh-action-pypi-publish](https://github.com/pypa/gh-action-pypi-publish) | `1.14.0` | `1.14.2` |
| [codecov/codecov-action](https://github.com/codecov/codecov-action) | `7.0.0` | `7.1.1` |
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

Updates `astral-sh/setup-uv` from 8.3.2 to 10.3.0
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
<li>Additional commits viewable in <a href="https://github.com/astral-sh/setup-uv/compare/11f9893b081a58869d3b5fccaea48c9e9e46f990...1c37ad07a6a961277cf70c0d37d6f313000f5884">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82d8aef1ef31`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.