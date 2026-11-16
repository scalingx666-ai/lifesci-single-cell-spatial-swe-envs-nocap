# Issue

**Title:** ci(dependabot): bump the actions group across 1 directory with 5 updates

## Description

Bumps the actions group with 5 updates in the / directory:

| Package | From | To |
| --- | --- | --- |
| [actions/checkout](https://github.com/actions/checkout) | `4` | `6` |
| [actions/setup-python](https://github.com/actions/setup-python) | `5` | `6` |
| [actions/upload-artifact](https://github.com/actions/upload-artifact) | `4` | `5` |
| [actions/download-artifact](https://github.com/actions/download-artifact) | `4` | `6` |
| [actions/github-script](https://github.com/actions/github-script) | `7` | `8` |

Updates `actions/checkout` from 4 to 6
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/releases">actions/checkout's releases</a>.</em></p>
<blockquote>
<h2>v6.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update README to include Node.js 24 support details and requirements by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2248</a></li>
<li>Persist creds to a separate file by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2286</a></li>
<li>v6-beta by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2298</a></li>
<li>update readme/changelog for v6 by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2311</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v5.0.0...v6.0.0">https://github.com/actions/checkout/compare/v5.0.0...v6.0.0</a></p>
<h2>v6-beta</h2>
<h2>What's Changed</h2>
<p>Updated persist-credentials to store the credentials under <code>$RUNNER_TEMP</code> instead of directly in the local git config.</p>
<p>This requires a minimum Actions Runner version of <a href="https://github.com/actions/runner/releases/tag/v2.329.0">v2.329.0</a> to access the persisted credentials for <a href="https://docs.github.com/en/actions/tutorials/use-containerized-services/create-a-docker-container-action">Docker container action</a> scenarios.</p>
<h2>v5.0.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Port v6 cleanup to v5 by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2301</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v5...v5.0.1">https://github.com/actions/checkout/compare/v5...v5.0.1</a></p>
<h2>v5.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update actions checkout to use node 24 by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2226</a></li>
<li>Prepare v5.0.0 release by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2238</a></li>
</ul>
<h2>⚠️ Minimum Compatible Runner Version</h2>
<p><strong>v2.327.1</strong><br />
<a href="https://github.com/actions/runner/releases/tag/v2.327.1">Release Notes</a></p>
<p>Make sure your runner is updated to this version or newer to use this release.</p>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v4...v5.0.0">https://github.com/actions/checkout/compare/v4...v5.0.0</a></p>
<h2>v4.3.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Port v6 cleanup to v4 by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2305</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v4...v4.3.1">https://github.com/actions/checkout/compare/v4...v4.3.1</a></p>
<h2>v4.3.0</h2>
<h2>What's Changed</h2>
<ul>
<li>docs: update README.md by <a href="https://github.com/motss"><code>@​motss</code></a> in <a href="">actions/checkout#1971</a></li>
<li>Add internal repos for checking out multiple repositories by <a href="https://github.com/mouismail"><code>@​mouismail</code></a> in <a href="">actions/checkout#1977</a></li>
<li>Documentation update - add recommended permissions to Readme by <a href="https://github.com/benwells"><code>@​benwells</code></a> in <a href="">actions/checkout#2043</a></li>
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
<h2>V6.0.0</h2>
<ul>
<li>Persist creds to a separate file by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2286</a></li>
<li>Update README to include Node.js 24 support details and requirements by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2248</a></li>
</ul>
<h2>V5.0.1</h2>
<ul>
<li>Port v6 cleanup to v5 by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2301</a></li>
</ul>
<h2>V5.0.0</h2>
<ul>
<li>Update actions checkout to use node 24 by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2226</a></li>
</ul>
<h2>V4.3.1</h2>
<ul>
<li>Port v6 cleanup to v4 by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2305</a></li>
</ul>
<h2>V4.3.0</h2>
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
<h2>v4.2.0</h2>
<ul>
<li>Add Ref and Commit outputs by <a href="https://github.com/lucacome"><code>@​lucacome</code></a> in <a href="">actions/checkout#1180</a></li>
<li>Dependency updates by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>- <a href="">actions/checkout#1777</a>, <a href="">actions/checkout#1872</a></li>
</ul>
<h2>v4.1.7</h2>
<ul>
<li>Bump the minor-npm-dependencies group across 1 directory with 4 updates by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/checkout#1739</a></li>
<li>Bump actions/checkout from 3 to 4 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/checkout#1697</a></li>
<li>Check out other refs/* by commit by <a href="https://github.com/orhantoy"><code>@​orhantoy</code></a> in <a href="">actions/checkout#1774</a></li>
<li>Pin actions/checkout's own workflows to a known, good, stable version. by <a href="https://github.com/jww3"><code>@​jww3</code></a> in <a href="">actions/checkout#1776</a></li>
</ul>
<h2>v4.1.6</h2>
<ul>
<li>Check platform to set archive extension appropriately by <a href="https://github.com/cory-miller"><code>@​cory-miller</code></a> in <a href="">actions/checkout#1732</a></li>
</ul>
<h2>v4.1.5</h2>
<ul>
<li>Update NPM dependencies by <a href="https://github.com/cory-miller"><code>@​cory-miller</code></a> in <a href="">actions/checkout#1703</a></li>
<li>Bump github/codeql-action from 2 to 3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/checkout#1694</a></li>
<li>Bump actions/setup-node from 1 to 4 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/checkout#1696</a></li>
<li>Bump actions/upload-artifact from 2 to 4 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/checkout#1695</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1af3b93</code></a> update readme/changelog for v6 (<a href="">#2311</a>)</li>
<li><a href=""><code>71cf226</code></a> v6-beta (<a href="">#2298</a>)</li>
<li><a href=""><code>069c695</code></a> Persist creds to a separate file (<a href="">#2286</a>)</li>
<li><a href=""><code>ff7abcd</code></a> Update README to include Node.js 24 support details and requirements (<a href="">#2248</a>)</li>
<li><a href=""><code>08c6903</code></a> Prepare v5.0.0 release (<a href="">#2238</a>)</li>
<li><a href=""><code>9f26565</code></a> Update actions checkout to use node 24 (<a href="">#2226</a>)</li>
<li>See full diff in <a href="https://github.com/actions/checkout/compare/v4...v6">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/setup-python` from 5 to 6
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>v6.0.0</h2>
<h2>What's Changed</h2>
<h3>Breaking Changes</h3>
<ul>
<li>Upgrade to node 24 by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/setup-python#1164</a></li>
</ul>
<p>Make sure your runner is on version v2.327.1 or later to ensure compatibility with this release. <a href="https://github.com/actions/runner/releases/tag/v2.327.1">See Release Notes</a></p>
<h3>Enhancements:</h3>
<ul>
<li>Add support for <code>pip-version</code>  by <a href="https://github.com/priyagupta108"><code>@​priyagupta108</code></a> in <a href="">actions/setup-python#1129</a></li>
<li>Enhance reading from .python-version by <a href="https://github.com/krystof-k"><code>@​krystof-k</code></a> in <a href="">actions/setup-python#787</a></li>
<li>Add version parsing from Pipfile by <a href="https://github.com/aradkdj"><code>@​aradkdj</code></a> in <a href="">actions/setup-python#1067</a></li>
</ul>
<h3>Bug fixes:</h3>
<ul>
<li>Clarify pythonLocation behaviour for PyPy and GraalPy in environment variables by <a href="https://github.com/aparnajyothi-y"><code>@​aparnajyothi-y</code></a> in <a href="">actions/setup-python#1183</a></li>
<li>Change missing cache directory error to warning  by <a href="https://github.com/aparnajyothi-y"><code>@​aparnajyothi-y</code></a> in <a href="">actions/setup-python#1182</a></li>
<li>Add Architecture-Specific PATH Management for Python with --user Flag on Windows by <a href="https://github.com/aparnajyothi-y"><code>@​aparnajyothi-y</code></a> in <a href="">actions/setup-python#1122</a></li>
<li>Include python version in PyPy python-version output by <a href="https://github.com/cdce8p"><code>@​cdce8p</code></a> in <a href="">actions/setup-python#1110</a></li>
<li>Update docs: clarification on pip authentication with setup-python by <a href="https://github.com/priya-kinthali"><code>@​priya-kinthali</code></a> in <a href="">actions/setup-python#1156</a></li>
</ul>
<h3>Dependency updates:</h3>
<ul>
<li>Upgrade idna from 2.9 to 3.7 in /<strong>tests</strong>/data by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-python#843</a></li>
<li>Upgrade form-data to fix critical vulnerabilities <a href="">#182</a> &amp; <a href="">#183</a> by <a href="https://github.com/aparnajyothi-y"><code>@​aparnajyothi-y</code></a> in <a href="">actions/setup-python#1163</a></li>
<li>Upgrade setuptools to 78.1.1 to fix path traversal vulnerability in PackageIndex.download by <a href="https://github.com/aparnajyothi-y"><code>@​aparnajyothi-y</code></a> in <a href="">actions/setup-python#1165</a></li>
<li>Upgrade actions/checkout from 4 to 5 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-python#1181</a></li>
<li>Upgrade <code>@​actions/tool-cache</code> from 2.0.1 to 2.0.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-python#1095</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/krystof-k"><code>@​krystof-k</code></a> made their first contribution in <a href="">actions/setup-python#787</a></li>
<li><a href="https://github.com/cdce8p"><code>@​cdce8p</code></a> made their first contribution in <a href="">actions/setup-python#1110</a></li>
<li><a href="https://github.com/aradkdj"><code>@​aradkdj</code></a> made their first contribution in <a href="">actions/setup-python#1067</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-python/compare/v5...v6.0.0">https://github.com/actions/setup-python/compare/v5...v6.0.0</a></p>
<h2>v5.6.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Workflow updates related to Ubuntu 20.04 by <a href="https://github.com/aparnajyothi-y"><code>@​aparnajyothi-y</code></a> in <a href="">actions/setup-python#1065</a></li>
<li>Fix for Candidate Not Iterable Error by <a href="https://github.com/aparnajyothi-y"><code>@​aparnajyothi-y</code></a> in <a href="">actions/setup-python#1082</a></li>
<li>Upgrade semver and <code>@​types/semver</code> by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-python#1091</a></li>
<li>Upgrade prettier from 2.8.8 to 3.5.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-python#1046</a></li>
<li>Upgrade ts-jest from 29.1.2 to 29.3.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-python#1081</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-python/compare/v5...v5.6.0">https://github.com/actions/setup-python/compare/v5...v5.6.0</a></p>
<h2>v5.5.0</h2>
<h2>What's Changed</h2>
<h3>Enhancements:</h3>
<ul>
<li>Support free threaded Python versions like '3.13t' by <a href="https://github.com/colesbury"><code>@​colesbury</code></a> in <a href="">actions/setup-python#973</a></li>
<li>Enhance Workflows: Include ubuntu-arm runners, Add e2e Testing for free threaded and Upgrade <code>@​action/cache</code> from 4.0.0 to 4.0.3 by <a href="https://github.com/priya-kinthali"><code>@​priya-kinthali</code></a> in <a href="">actions/setup-python#1056</a></li>
<li>Add support for .tool-versions file in setup-python by <a href="https://github.com/mahabaleshwars"><code>@​mahabaleshwars</code></a> in <a href="">actions/setup-python#1043</a></li>
</ul>
<h3>Bug fixes:</h3>
<ul>
<li>Fix architecture for pypy on Linux ARM64 by <a href="https://github.com/mayeut"><code>@​mayeut</code></a> in <a href="">actions/setup-python#1011</a>
This update maps arm64 to aarch64 for Linux ARM64 PyPy installations.</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>83679a8</code></a> Bump <code>@​types/node</code> from 24.1.0 to 24.9.1 and update macos-13 to macos-15-intel ...</li>
<li><a href=""><code>bfc4944</code></a> Bump prettier from 3.5.3 to 3.6.2 (<a href="">#1234</a>)</li>
<li><a href=""><code>97aeb3e</code></a> Bump requests from 2.32.2 to 2.32.4 in /<strong>tests</strong>/data (<a href="">#1130</a>)</li>
<li><a href=""><code>443da59</code></a> Bump actions/publish-action from 0.3.0 to 0.4.0 &amp; Documentation update for pi...</li>
<li><a href=""><code>cfd55ca</code></a> graalpy: add graalpy early-access and windows builds (<a href="">#880</a>)</li>
<li><a href=""><code>bba65e5</code></a> Bump typescript from 5.4.2 to 5.9.3 and update docs/advanced-usage.md (<a href="">#1094</a>)</li>
<li><a href=""><code>18566f8</code></a> Improve wording and &quot;fix example&quot; (remove 3.13) on testing against pre-releas...</li>
<li><a href=""><code>2e3e4b1</code></a> Add support for pip-install input (<a href="">#1201</a>)</li>
<li><a href=""><code>4267e28</code></a> Bump urllib3 from 1.26.19 to 2.5.0 in /<strong>tests</strong>/data and document breaking c...</li>
<li><a href=""><code>e797f83</code></a> Upgrade to node 24 (<a href="">#1164</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/setup-python/compare/v5...v6">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/upload-artifact` from 4 to 5
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/upload-artifact/releases">actions/upload-artifact's releases</a>.</em></p>
<blockquote>
<h2>v5.0.0</h2>
<h2>What's Changed</h2>
<p><strong>BREAKING CHANGE:</strong> this update supports Node <code>v24.x</code>. This is not a breaking change per-se but we're treating it as such.</p>
<ul>
<li>Update README.md by <a href="https://github.com/GhadimiR"><code>@​GhadimiR</code></a> in <a href="">actions/upload-artifact#681</a></li>
<li>Update README.md by <a href="https://github.com/nebuk89"><code>@​nebuk89</code></a> in <a href="">actions/upload-artifact#712</a></li>
<li>Readme: spell out the first use of GHES by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/upload-artifact#727</a></li>
<li>Update GHES guidance to include reference to Node 20 version by <a href="https://github.com/patrikpolyak"><code>@​patrikpolyak</code></a> in <a href="">actions/upload-artifact#725</a></li>
<li>Bump <code>@actions/artifact</code> to <code>v4.0.0</code></li>
<li>Prepare <code>v5.0.0</code> by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/upload-artifact#734</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/GhadimiR"><code>@​GhadimiR</code></a> made their first contribution in <a href="">actions/upload-artifact#681</a></li>
<li><a href="https://github.com/nebuk89"><code>@​nebuk89</code></a> made their first contribution in <a href="">actions/upload-artifact#712</a></li>
<li><a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> made their first contribution in <a href="">actions/upload-artifact#727</a></li>
<li><a href="https://github.com/patrikpolyak"><code>@​patrikpolyak</code></a> made their first contribution in <a href="">actions/upload-artifact#725</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/upload-artifact/compare/v4...v5.0.0">https://github.com/actions/upload-artifact/compare/v4...v5.0.0</a></p>
<h2>v4.6.2</h2>
<h2>What's Changed</h2>
<ul>
<li>Update to use artifact 2.3.2 package &amp; prepare for new upload-artifact release by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/upload-artifact#685</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> made their first contribution in <a href="">actions/upload-artifact#685</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/upload-artifact/compare/v4...v4.6.2">https://github.com/actions/upload-artifact/compare/v4...v4.6.2</a></p>
<h2>v4.6.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Update to use artifact 2.2.2 package by <a href="https://github.com/yacaovsnc"><code>@​yacaovsnc</code></a> in <a href="">actions/upload-artifact#673</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/upload-artifact/compare/v4...v4.6.1">https://github.com/actions/upload-artifact/compare/v4...v4.6.1</a></p>
<h2>v4.6.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Expose env vars to control concurrency and timeout by <a href="https://github.com/yacaovsnc"><code>@​yacaovsnc</code></a> in <a href="">actions/upload-artifact#662</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/upload-artifact/compare/v4...v4.6.0">https://github.com/actions/upload-artifact/compare/v4...v4.6.0</a></p>
<h2>v4.5.0</h2>
<h2>What's Changed</h2>
<ul>
<li>fix: deprecated <code>Node.js</code> version in action by <a href="https://github.com/hamirmahal"><code>@​hamirmahal</code></a> in <a href="">actions/upload-artifact#578</a></li>
<li>Add new <code>artifact-digest</code> output by <a href="https://github.com/bdehamer"><code>@​bdehamer</code></a> in <a href="">actions/upload-artifact#656</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/hamirmahal"><code>@​hamirmahal</code></a> made their first contribution in <a href="">actions/upload-artifact#578</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>330a01c</code></a> Merge pull request <a href="">#734</a> from actions/danwkennedy/prepare-5.0.0</li>
<li><a href=""><code>03f2824</code></a> Update <code>github.dep.yml</code></li>
<li><a href=""><code>905a1ec</code></a> Prepare <code>v5.0.0</code></li>
<li><a href=""><code>2d9f9cd</code></a> Merge pull request <a href="">#725</a> from patrikpolyak/patch-1</li>
<li><a href=""><code>9687587</code></a> Merge branch 'main' into patch-1</li>
<li><a href=""><code>2848b2c</code></a> Merge pull request <a href="">#727</a> from danwkennedy/patch-1</li>
<li><a href=""><code>9b51177</code></a> Spell out the first use of GHES</li>
<li><a href=""><code>cd231ca</code></a> Update GHES guidance to include reference to Node 20 version</li>
<li><a href=""><code>de65e23</code></a> Merge pull request <a href="">#712</a> from actions/nebuk89-patch-1</li>
<li><a href=""><code>8747d8c</code></a> Update README.md</li>
<li>Additional commits viewable in <a href="https://github.com/actions/upload-artifact/compare/v4...v5">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/download-artifact` from 4 to 6
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/download-artifact/releases">actions/download-artifact's releases</a>.</em></p>
<blockquote>
<h2>v6.0.0</h2>
<h2>What's Changed</h2>
<p><strong>BREAKING CHANGE:</strong> this update supports Node <code>v24.x</code>. This is not a breaking change per-se but we're treating it as such.</p>
<ul>
<li>Update README for download-artifact v5 changes by <a href="https://github.com/yacaovsnc"><code>@​yacaovsnc</code></a> in <a href="">actions/download-artifact#417</a></li>
<li>Update README with artifact extraction details by <a href="https://github.com/yacaovsnc"><code>@​yacaovsnc</code></a> in <a href="">actions/download-artifact#424</a></li>
<li>Readme: spell out the first use of GHES by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/download-artifact#431</a></li>
<li>Bump <code>@actions/artifact</code> to <code>v4.0.0</code></li>
<li>Prepare <code>v6.0.0</code> by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/download-artifact#438</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> made their first contribution in <a href="">actions/download-artifact#431</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/download-artifact/compare/v5...v6.0.0">https://github.com/actions/download-artifact/compare/v5...v6.0.0</a></p>
<h2>v5.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update README.md by <a href="https://github.com/nebuk89"><code>@​nebuk89</code></a> in <a href="">actions/download-artifact#407</a></li>
<li>BREAKING fix: inconsistent path behavior for single artifact downloads by ID by <a href="https://github.com/GrantBirki"><code>@​GrantBirki</code></a> in <a href="">actions/download-artifact#416</a></li>
</ul>
<h2>v5.0.0</h2>
<h3>🚨 Breaking Change</h3>
<p>This release fixes an inconsistency in path behavior for single artifact downloads by ID. <strong>If you're downloading single artifacts by ID, the output path may change.</strong></p>
<h4>What Changed</h4>
<p>Previously, <strong>single artifact downloads</strong> behaved differently depending on how you specified the artifact:</p>
<ul>
<li><strong>By name</strong>: <code>name: my-artifact</code> → extracted to <code>path/</code> (direct)</li>
<li><strong>By ID</strong>: <code>artifact-ids: 12345</code> → extracted to <code>path/my-artifact/</code> (nested)</li>
</ul>
<p>Now both methods are consistent:</p>
<ul>
<li><strong>By name</strong>: <code>name: my-artifact</code> → extracted to <code>path/</code> (unchanged)</li>
<li><strong>By ID</strong>: <code>artifact-ids: 12345</code> → extracted to <code>path/</code> (fixed - now direct)</li>
</ul>
<h4>Migration Guide</h4>
<h5>✅ No Action Needed If:</h5>
<ul>
<li>You download artifacts by <strong>name</strong></li>
<li>You download <strong>multiple</strong> artifacts by ID</li>
<li>You already use <code>merge-multiple: true</code> as a workaround</li>
</ul>
<h5>⚠️ Action Required If:</h5>
<p>You download <strong>single artifacts by ID</strong> and your workflows expect the nested directory structure.</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>018cc2c</code></a> Merge pull request <a href="">#438</a> from actions/danwkennedy/prepare-6.0.0</li>
<li><a href=""><code>815651c</code></a> Revert &quot;Remove <code>github.dep.yml</code>&quot;</li>
<li><a href=""><code>bb3a066</code></a> Remove <code>github.dep.yml</code></li>
<li><a href=""><code>fa1ce46</code></a> Prepare <code>v6.0.0</code></li>
<li><a href=""><code>4a24838</code></a> Merge pull request <a href="">#431</a> from danwkennedy/patch-1</li>
<li><a href=""><code>5e3251c</code></a> Readme: spell out the first use of GHES</li>
<li><a href=""><code>abefc31</code></a> Merge pull request <a href="">#424</a> from actions/yacaovsnc/update_readme</li>
<li><a href=""><code>ac43a60</code></a> Update README with artifact extraction details</li>
<li><a href=""><code>de96f46</code></a> Merge pull request <a href="">#417</a> from actions/yacaovsnc/update_readme</li>
<li><a href=""><code>7993cb4</code></a> Remove migration guide for artifact download changes</li>
<li>Additional commits viewable in <a href="https://github.com/actions/download-artifact/compare/v4...v6">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/github-script` from 7 to 8
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/github-script/releases">actions/github-script's releases</a>.</em></p>
<blockquote>
<h2>v8.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update Node.js version support to 24.x by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/github-script#637</a></li>
<li>README for updating actions/github-script from v7 to v8 by <a href="https://github.com/sneha-krip"><code>@​sneha-krip</code></a> in <a href="">actions/github-script#653</a></li>
</ul>
<h2>⚠️ Minimum Compatible Runner Version</h2>
<p><strong>v2.327.1</strong><br />
<a href="https://github.com/actions/runner/releases/tag/v2.327.1">Release Notes</a></p>
<p>Make sure your runner is updated to this version or newer to use this release.</p>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> made their first contribution in <a href="">actions/github-script#637</a></li>
<li><a href="https://github.com/sneha-krip"><code>@​sneha-krip</code></a> made their first contribution in <a href="">actions/github-script#653</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/github-script/compare/v7.1.0...v8.0.0">https://github.com/actions/github-script/compare/v7.1.0...v8.0.0</a></p>
<h2>v7.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Upgrade husky to v9 by <a href="https://github.com/benelan"><code>@​benelan</code></a> in <a href="">actions/github-script#482</a></li>
<li>Add workflow file for publishing releases to immutable action package by <a href="https://github.com/Jcambass"><code>@​Jcambass</code></a> in <a href="">actions/github-script#485</a></li>
<li>Upgrade IA Publish by <a href="https://github.com/Jcambass"><code>@​Jcambass</code></a> in <a href="">actions/github-script#486</a></li>
<li>Fix workflow status badges by <a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> in <a href="">actions/github-script#497</a></li>
<li>Update usage of <code>actions/upload-artifact</code> by <a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> in <a href="">actions/github-script#512</a></li>
<li>Clear up package name confusion by <a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> in <a href="">actions/github-script#514</a></li>
<li>Update dependencies with <code>npm audit fix</code> by <a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> in <a href="">actions/github-script#515</a></li>
<li>Specify that the used script is JavaScript by <a href="https://github.com/timotk"><code>@​timotk</code></a> in <a href="">actions/github-script#478</a></li>
<li>chore: Add Dependabot for NPM and Actions by <a href="https://github.com/nschonni"><code>@​nschonni</code></a> in <a href="">actions/github-script#472</a></li>
<li>Define <code>permissions</code> in workflows and update actions by <a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> in <a href="">actions/github-script#531</a></li>
<li>chore: Add Dependabot for .github/actions/install-dependencies by <a href="https://github.com/nschonni"><code>@​nschonni</code></a> in <a href="">actions/github-script#532</a></li>
<li>chore: Remove .vscode settings by <a href="https://github.com/nschonni"><code>@​nschonni</code></a> in <a href="">actions/github-script#533</a></li>
<li>ci: Use github/setup-licensed by <a href="https://github.com/nschonni"><code>@​nschonni</code></a> in <a href="">actions/github-script#473</a></li>
<li>make octokit instance available as octokit on top of github, to make it easier to seamlessly copy examples from GitHub rest api or octokit documentations by <a href="https://github.com/iamstarkov"><code>@​iamstarkov</code></a> in <a href="">actions/github-script#508</a></li>
<li>Remove <code>octokit</code> README updates for v7 by <a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> in <a href="">actions/github-script#557</a></li>
<li>docs: add &quot;exec&quot; usage examples by <a href="https://github.com/neilime"><code>@​neilime</code></a> in <a href="">actions/github-script#546</a></li>
<li>Bump ruby/setup-ruby from 1.213.0 to 1.222.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/github-script#563</a></li>
<li>Bump ruby/setup-ruby from 1.222.0 to 1.229.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/github-script#575</a></li>
<li>Clearly document passing inputs to the <code>script</code> by <a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> in <a href="">actions/github-script#603</a></li>
<li>Update README.md by <a href="https://github.com/nebuk89"><code>@​nebuk89</code></a> in <a href="">actions/github-script#610</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/benelan"><code>@​benelan</code></a> made their first contribution in <a href="">actions/github-script#482</a></li>
<li><a href="https://github.com/Jcambass"><code>@​Jcambass</code></a> made their first contribution in <a href="">actions/github-script#485</a></li>
<li><a href="https://github.com/timotk"><code>@​timotk</code></a> made their first contribution in <a href="">actions/github-script#478</a></li>
<li><a href="https://github.com/iamstarkov"><code>@​iamstarkov</code></a> made their first contribution in <a href="">actions/github-script#508</a></li>
<li><a href="https://github.com/neilime"><code>@​neilime</code></a> made their first contribution in <a href="">actions/github-script#546</a></li>
<li><a href="https://github.com/nebuk89"><code>@​nebuk89</code></a> made their first contribution in <a href="">actions/github-script#610</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/github-script/compare/v7...v7.1.0">https://github.com/actions/github-script/compare/v7...v7.1.0</a></p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ed59741</code></a> Merge pull request <a href="">#653</a> from actions/sneha-krip/readme-for-v8</li>
<li><a href=""><code>2dc352e</code></a> Bold minimum Actions Runner version in README</li>
<li><a href=""><code>01e118c</code></a> Update README for Node 24 runtime requirements</li>
<li><a href=""><code>8b222ac</code></a> Apply suggestion from <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a></li>
<li><a href=""><code>adc0eea</code></a> README for updating actions/github-script from v7 to v8</li>
<li><a href=""><code>20fe497</code></a> Merge pull request <a href="">#637</a> from actions/node24</li>
<li><a href=""><code>e7b7f22</code></a> update licenses</li>
<li><a href=""><code>2c81ba0</code></a> Update Node.js version support to 24.x</li>
<li>See full diff in <a href="https://github.com/actions/github-script/compare/v7...v8">compare view</a></li>
</ul>
</details>
<br />

You can trigger a rebase of this PR by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

> **Note**
> Automatic rebases have been disabled on this pull request as it has been open for over 30 days.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b39fc55104ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.