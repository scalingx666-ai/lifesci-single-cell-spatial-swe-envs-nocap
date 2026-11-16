# Issue

**Title:** build(deps): bump the actions group with 3 updates

## Description

Bumps the actions group with 3 updates: [actions/checkout](https://github.com/actions/checkout), [actions/upload-artifact](https://github.com/actions/upload-artifact) and [codecov/codecov-action](https://github.com/codecov/codecov-action).

Updates `actions/checkout` from 6 to 7
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/releases">actions/checkout's releases</a>.</em></p>
<blockquote>
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
<li>Fix tag handling: preserve annotations and explicit fetch-tags by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2356</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v6.0.1...v6.0.2">https://github.com/actions/checkout/compare/v6.0.1...v6.0.2</a></p>
<h2>v6.0.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Update all references from v5 and v4 to v6 by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2314</a></li>
<li>Add worktree support for persist-credentials includeIf by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2327</a></li>
<li>Clarify v6 README by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2328</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v6...v6.0.1">https://github.com/actions/checkout/compare/v6...v6.0.1</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/blob/main/CHANGELOG.md">actions/checkout's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<h2>v7.0.0</h2>
<ul>
<li>Block checking out fork PR for pull_request_target and workflow_run by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2454</a></li>
<li>Bump actions/publish-immutable-action from 0.0.3 to 0.0.4 in the minor-actions-dependencies group across 1 directory by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/checkout#2458</a></li>
<li>Bump flatted from 3.3.1 to 3.4.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/checkout#2460</a></li>
<li>Bump js-yaml from 4.1.0 to 4.2.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/checkout#2461</a></li>
<li>Bump <code>@​actions/core</code> and <code>@​actions/tool-cache</code> and Remove uuid by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/checkout#2459</a></li>
<li>upgrade module to esm and update dependencies by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2463</a></li>
<li>Bump the minor-npm-dependencies group across 1 directory with 3 updates by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/checkout#2462</a></li>
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
<li><a href=""><code>9c091bb</code></a> update error wording (<a href="">#2467</a>)</li>
<li><a href=""><code>1044a6d</code></a> getting ready for checkout v7 release (<a href="">#2464</a>)</li>
<li><a href=""><code>f028218</code></a> Bump the minor-npm-dependencies group across 1 directory with 3 updates (<a href="">#2462</a>)</li>
<li><a href=""><code>d914b26</code></a> upgrade module to esm and update dependencies (<a href="">#2463</a>)</li>
<li><a href=""><code>537c7ef</code></a> Bump <code>@​actions/core</code> and <code>@​actions/tool-cache</code> and Remove uuid (<a href="">#2459</a>)</li>
<li><a href=""><code>130a169</code></a> Bump js-yaml from 4.1.0 to 4.2.0 (<a href="">#2461</a>)</li>
<li><a href=""><code>7d09575</code></a> Bump flatted from 3.3.1 to 3.4.2 (<a href="">#2460</a>)</li>
<li><a href=""><code>0f9f3aa</code></a> Bump actions/publish-immutable-action (<a href="">#2458</a>)</li>
<li><a href=""><code>f9e715a</code></a> block checking out fork pr for pull_request_target and workflow_run (<a href="">#2454</a>)</li>
<li>See full diff in <a href="https://github.com/actions/checkout/compare/v6...v7">compare view</a></li>
</ul>
</details>
<br />

Updates `actions/upload-artifact` from 4 to 7
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/upload-artifact/releases">actions/upload-artifact's releases</a>.</em></p>
<blockquote>
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
<p><strong>BREAKING CHANGE:</strong> this update supports Node <code>v24.x</code>. This is not a breaking change per-se but we're treating it as such.</p>
<ul>
<li>Update README.md by <a href="https://github.com/GhadimiR"><code>@​GhadimiR</code></a> in <a href="">actions/upload-artifact#681</a></li>
<li>Update README.md by <a href="https://github.com/nebuk89"><code>@​nebuk89</code></a> in <a href="">actions/upload-artifact#712</a></li>
<li>Readme: spell out the first use of GHES by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/upload-artifact#727</a></li>
<li>Update GHES guidance to include reference to Node 20 version by <a href="https://github.com/patrikpolyak"><code>@​patrikpolyak</code></a> in <a href="">actions/upload-artifact#725</a></li>
<li>Bump <code>@actions/artifact</code> to <code>v4.0.0</code></li>
<li>Prepare <code>v5.0.0</code> by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/upload-artifact#734</a></li>
</ul>
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
<li>Additional commits viewable in <a href="https://github.com/actions/upload-artifact/compare/v4...v7">compare view</a></li>
</ul>
</details>
<br />

Updates `codecov/codecov-action` from 6 to 7
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/releases">codecov/codecov-action's releases</a>.</em></p>
<blockquote>
<h2>v7.0.0</h2>
<p>⚠️ Due to migration issues with keybase, we are unable to update our keys under the <code>codecovsecurity</code> account. We have deleted the account and are using <code>codecovsecops</code> with the original gpg key</p>
<h2>What's Changed</h2>
<ul>
<li>ci: remove Enforce License Compliance workflow by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1950</a></li>
<li>chore(release): 7.0.0 by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1957</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v6.0.1...v7.0.0">https://github.com/codecov/codecov-action/compare/v6.0.1...v7.0.0</a></p>
<h2>v6.0.2</h2>
<p>This is a copy of the <code>v7.0.0</code> release to make updates easier</p>
<h2>What's Changed</h2>
<ul>
<li>ci: remove Enforce License Compliance workflow by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1950</a></li>
<li>chore(release): 7.0.0 by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1957</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v6.0.1...v6.0.2">https://github.com/codecov/codecov-action/compare/v6.0.1...v6.0.2</a></p>
<h2>v6.0.1</h2>
<h2>What's Changed</h2>
<ul>
<li>fix: prevent template injection in run: steps (VULN-1652) by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1947</a></li>
<li>chore(release): 6.0.1 by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1949</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v6.0.0...v6.0.1">https://github.com/codecov/codecov-action/compare/v6.0.0...v6.0.1</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/blob/main/CHANGELOG.md">codecov/codecov-action's changelog</a>.</em></p>
<blockquote>
<h2>v5.5.2</h2>
<h3>What's Changed</h3>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v5.5.1..v5.5.2">https://github.com/codecov/codecov-action/compare/v5.5.1..v5.5.2</a></p>
<h2>v5.5.1</h2>
<h3>What's Changed</h3>
<ul>
<li>fix: overwrite pr number on fork by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1871</a></li>
<li>build(deps): bump actions/checkout from 4.2.2 to 5.0.0 by <code>@​app/dependabot</code> in <a href="">codecov/codecov-action#1868</a></li>
<li>build(deps): bump github/codeql-action from 3.29.9 to 3.29.11 by <code>@​app/dependabot</code> in <a href="">codecov/codecov-action#1867</a></li>
<li>fix: update to use local app/ dir by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1872</a></li>
<li>docs: fix typo in README by <a href="https://github.com/datalater"><code>@​datalater</code></a> in <a href="">codecov/codecov-action#1866</a></li>
<li>Document a <code>codecov-cli</code> version reference example by <a href="https://github.com/webknjaz"><code>@​webknjaz</code></a> in <a href="">codecov/codecov-action#1774</a></li>
<li>build(deps): bump github/codeql-action from 3.28.18 to 3.29.9 by <code>@​app/dependabot</code> in <a href="">codecov/codecov-action#1861</a></li>
<li>build(deps): bump ossf/scorecard-action from 2.4.1 to 2.4.2 by <code>@​app/dependabot</code> in <a href="">codecov/codecov-action#1833</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v5.5.0..v5.5.1">https://github.com/codecov/codecov-action/compare/v5.5.0..v5.5.1</a></p>
<h2>v5.5.0</h2>
<h3>What's Changed</h3>
<ul>
<li>feat: upgrade wrapper to 0.2.4 by <a href="https://github.com/jviall"><code>@​jviall</code></a> in <a href="">codecov/codecov-action#1864</a></li>
<li>Pin actions/github-script by Git SHA by <a href="https://github.com/martincostello"><code>@​martincostello</code></a> in <a href="">codecov/codecov-action#1859</a></li>
<li>fix: check reqs exist by <a href="https://github.com/joseph-sentry"><code>@​joseph-sentry</code></a> in <a href="">codecov/codecov-action#1835</a></li>
<li>fix: Typo in README by <a href="https://github.com/spalmurray"><code>@​spalmurray</code></a> in <a href="">codecov/codecov-action#1838</a></li>
<li>docs: Refine OIDC docs by <a href="https://github.com/spalmurray"><code>@​spalmurray</code></a> in <a href="">codecov/codecov-action#1837</a></li>
<li>build(deps): bump github/codeql-action from 3.28.17 to 3.28.18 by <code>@​app/dependabot</code> in <a href="">codecov/codecov-action#1829</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v5.4.3..v5.5.0">https://github.com/codecov/codecov-action/compare/v5.4.3..v5.5.0</a></p>
<h2>v5.4.3</h2>
<h3>What's Changed</h3>
<ul>
<li>build(deps): bump github/codeql-action from 3.28.13 to 3.28.17 by <code>@​app/dependabot</code> in <a href="">codecov/codecov-action#1822</a></li>
<li>fix: OIDC on forks by <a href="https://github.com/joseph-sentry"><code>@​joseph-sentry</code></a> in <a href="">codecov/codecov-action#1823</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v5.4.2..v5.4.3">https://github.com/codecov/codecov-action/compare/v5.4.2..v5.4.3</a></p>
<h2>v5.4.2</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/codecov/codecov-action/compare/v6...v7">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4719939de61c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.