# Issue

**Title:** build(deps): bump the github-actions-patch-minor group across 1 directory with 5 updates

## Description

Bumps the github-actions-patch-minor group with 5 updates in the / directory:

| Package | From | To |
| --- | --- | --- |
| [actions/checkout](https://github.com/actions/checkout) | `6.0.2` | `6.0.3` |
| [docker/setup-buildx-action](https://github.com/docker/setup-buildx-action) | `4.0.0` | `4.1.0` |
| [docker/login-action](https://github.com/docker/login-action) | `4.1.0` | `4.2.0` |
| [docker/build-push-action](https://github.com/docker/build-push-action) | `7.1.0` | `7.2.0` |
| [docker/metadata-action](https://github.com/docker/metadata-action) | `6.0.0` | `6.1.0` |

Updates `actions/checkout` from 6.0.2 to 6.0.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/releases">actions/checkout's releases</a>.</em></p>
<blockquote>
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
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/blob/main/CHANGELOG.md">actions/checkout's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
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
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>df4cb1c</code></a> Update changelog for v6.0.3 (<a href="">#2446</a>)</li>
<li><a href=""><code>1cce339</code></a> Fix checkout init for SHA-256 repositories (<a href="">#2439</a>)</li>
<li><a href=""><code>900f221</code></a> fix: expand merge commit SHA regex and add SHA-256 test cases (<a href="">#2414</a>)</li>
<li><a href=""><code>0c366fd</code></a> Update changelog (<a href="">#2357</a>)</li>
<li>See full diff in <a href="https://github.com/actions/checkout/compare/de0fac2e4500dabe0009e67214ff5f5447ce83dd...df4cb1c069e1874edd31b4311f1884172cec0e10">compare view</a></li>
</ul>
</details>
<br />

Updates `docker/setup-buildx-action` from 4.0.0 to 4.1.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/setup-buildx-action/releases">docker/setup-buildx-action's releases</a>.</em></p>
<blockquote>
<h2>v4.1.0</h2>
<ul>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.79.0 to 0.90.0 in <a href="">docker/setup-buildx-action#489</a></li>
<li>Bump brace-expansion from 1.1.12 to 5.0.6 in <a href="">docker/setup-buildx-action#547</a> <a href="">docker/setup-buildx-action#508</a></li>
<li>Bump fast-xml-builder from 1.0.0 to 1.2.0 in <a href="">docker/setup-buildx-action#540</a></li>
<li>Bump fast-xml-parser from 5.4.2 to 5.8.0 in <a href="">docker/setup-buildx-action#496</a></li>
<li>Bump flatted from 3.3.3 to 3.4.2 in <a href="">docker/setup-buildx-action#499</a></li>
<li>Bump glob from 10.3.12 to 13.0.6 in <a href="">docker/setup-buildx-action#495</a></li>
<li>Bump handlebars from 4.7.8 to 4.7.9 in <a href="">docker/setup-buildx-action#504</a></li>
<li>Bump lodash from 4.17.23 to 4.18.1 in <a href="">docker/setup-buildx-action#523</a></li>
<li>Bump picomatch from 4.0.3 to 4.0.4 in <a href="">docker/setup-buildx-action#503</a></li>
<li>Bump postcss from 8.5.6 to 8.5.10 in <a href="">docker/setup-buildx-action#537</a></li>
<li>Bump tar from 6.2.1 to 7.5.15 in <a href="">docker/setup-buildx-action#545</a></li>
<li>Bump undici from 6.23.0 to 6.25.0 in <a href="">docker/setup-buildx-action#492</a></li>
<li>Bump vite from 7.3.1 to 7.3.2 in <a href="">docker/setup-buildx-action#520</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v4.0.0...v4.1.0">https://github.com/docker/setup-buildx-action/compare/v4.0.0...v4.1.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d7f5e7f</code></a> Merge pull request <a href="">#489</a> from docker/dependabot/npm_and_yarn/docker/actions-to...</li>
<li><a href=""><code>92bc5c9</code></a> chore: update generated content</li>
<li><a href=""><code>da11e35</code></a> build(deps): bump <code>@​docker/actions-toolkit</code> from 0.79.0 to 0.90.0</li>
<li><a href=""><code>f021e16</code></a> Merge pull request <a href="">#492</a> from docker/dependabot/npm_and_yarn/undici-6.24.1</li>
<li><a href=""><code>b5af94f</code></a> chore: update generated content</li>
<li><a href=""><code>16ad977</code></a> build(deps): bump undici from 6.23.0 to 6.25.0</li>
<li><a href=""><code>d7a12d7</code></a> Merge pull request <a href="">#495</a> from docker/dependabot/npm_and_yarn/glob-10.5.0</li>
<li><a href=""><code>28ff27d</code></a> build(deps): bump glob from 10.3.12 to 13.0.6</li>
<li><a href=""><code>daf436b</code></a> Merge pull request <a href="">#496</a> from docker/dependabot/npm_and_yarn/fast-xml-parser-5...</li>
<li><a href=""><code>9725348</code></a> chore: update generated content</li>
<li>Additional commits viewable in <a href="https://github.com/docker/setup-buildx-action/compare/4d04d5d9486b7bd6fa91e7baf45bbb4f8b9deedd...d7f5e7f509e45cec5c76c4d5afdd7de93d0b3df5">compare view</a></li>
</ul>
</details>
<br />

Updates `docker/login-action` from 4.1.0 to 4.2.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/login-action/releases">docker/login-action's releases</a>.</em></p>
<blockquote>
<h2>v4.2.0</h2>
<ul>
<li>Bump <code>@​actions/core</code> from 3.0.0 to 3.0.1 in <a href="">docker/login-action#976</a></li>
<li>Bump <code>@​aws-sdk/client-ecr</code> and <code>@​aws-sdk/client-ecr-public</code> to 3.1050.0 in <a href="">docker/login-action#960</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.86.0 to 0.90.0 in <a href="">docker/login-action#970</a></li>
<li>Bump brace-expansion from 2.0.1 to 5.0.6 in <a href="">docker/login-action#993</a></li>
<li>Bump fast-xml-builder from 1.1.4 to 1.2.0 in <a href="">docker/login-action#985</a></li>
<li>Bump fast-xml-parser from 5.3.6 to 5.8.0 in <a href="">docker/login-action#963</a></li>
<li>Bump http-proxy-agent and https-proxy-agent to 9.0.0 in <a href="">docker/login-action#961</a></li>
<li>Bump postcss from 8.5.6 to 8.5.10 in <a href="">docker/login-action#979</a></li>
<li>Bump tar from 6.2.1 to 7.5.15 in <a href="">docker/login-action#991</a></li>
<li>Bump vite from 7.3.1 to 7.3.3 in <a href="">docker/login-action#986</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v4.1.0...v4.2.0">https://github.com/docker/login-action/compare/v4.1.0...v4.2.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>650006c</code></a> Merge pull request <a href="">#960</a> from docker/dependabot/npm_and_yarn/aws-sdk-dependenc...</li>
<li><a href=""><code>99df1a3</code></a> chore: update generated content</li>
<li><a href=""><code>3ab375f</code></a> build(deps): bump the aws-sdk-dependencies group across 1 directory with 2 up...</li>
<li><a href=""><code>39d8580</code></a> Merge pull request <a href="">#970</a> from docker/dependabot/npm_and_yarn/docker/actions-to...</li>
<li><a href=""><code>4eefcd3</code></a> chore: update generated content</li>
<li><a href=""><code>56d092c</code></a> build(deps): bump <code>@​docker/actions-toolkit</code> from 0.86.0 to 0.90.0</li>
<li><a href=""><code>e2e31ca</code></a> Merge pull request <a href="">#976</a> from docker/dependabot/npm_and_yarn/actions/core-3.0.1</li>
<li><a href=""><code>0bced94</code></a> chore: update generated content</li>
<li><a href=""><code>3e75a0f</code></a> build(deps): bump <code>@​actions/core</code> from 3.0.0 to 3.0.1</li>
<li><a href=""><code>365bebd</code></a> Merge pull request <a href="">#984</a> from docker/dependabot/github_actions/aws-actions/con...</li>
<li>Additional commits viewable in <a href="https://github.com/docker/login-action/compare/4907a6ddec9925e35a0a9e82d7399ccc52663121...650006c6eb7dba73a995cc03b0b2d7f5ca915bee">compare view</a></li>
</ul>
</details>
<br />

Updates `docker/build-push-action` from 7.1.0 to 7.2.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/build-push-action/releases">docker/build-push-action's releases</a>.</em></p>
<blockquote>
<h2>v7.2.0</h2>
<ul>
<li>Bump <code>@​actions/core</code> from 3.0.0 to 3.0.1 in <a href="">docker/build-push-action#1525</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.87.0 to 0.90.0 in <a href="">docker/build-push-action#1517</a></li>
<li>Bump brace-expansion from 2.0.2 to 5.0.6 in <a href="">docker/build-push-action#1534</a></li>
<li>Bump fast-xml-builder from 1.1.4 to 1.2.0 in <a href="">docker/build-push-action#1529</a></li>
<li>Bump fast-xml-parser from 5.5.7 to 5.8.0 in <a href="">docker/build-push-action#1521</a></li>
<li>Bump postcss from 8.5.6 to 8.5.10 in <a href="">docker/build-push-action#1526</a></li>
<li>Bump tar from 6.2.1 to 7.5.15 in <a href="">docker/build-push-action#1533</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/build-push-action/compare/v7.1.0...v7.2.0">https://github.com/docker/build-push-action/compare/v7.1.0...v7.2.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>f9f3042</code></a> Merge pull request <a href="">#1517</a> from docker/dependabot/npm_and_yarn/docker/actions-t...</li>
<li><a href=""><code>812d5fd</code></a> chore: update generated content</li>
<li><a href=""><code>b6f6693</code></a> chore(deps): Bump <code>@​docker/actions-toolkit</code> from 0.87.0 to 0.90.0</li>
<li><a href=""><code>c1c626e</code></a> Merge pull request <a href="">#1525</a> from docker/dependabot/npm_and_yarn/actions/core-3.0.1</li>
<li><a href=""><code>51bb284</code></a> chore: update generated content</li>
<li><a href=""><code>5f7884d</code></a> chore(deps): Bump <code>@​actions/core</code> from 3.0.0 to 3.0.1</li>
<li><a href=""><code>e01deff</code></a> Merge pull request <a href="">#1521</a> from docker/dependabot/npm_and_yarn/fast-xml-parser-...</li>
<li><a href=""><code>3804d49</code></a> chore: update generated content</li>
<li><a href=""><code>71e8947</code></a> chore(deps): Bump fast-xml-parser from 5.5.7 to 5.8.0</li>
<li><a href=""><code>4925ad2</code></a> Merge pull request <a href="">#1526</a> from docker/dependabot/npm_and_yarn/postcss-8.5.10</li>
<li>Additional commits viewable in <a href="https://github.com/docker/build-push-action/compare/bcafcacb16a39f128d818304e6c9c0c18556b85f...f9f3042f7e2789586610d6e8b85c8f03e5195baf">compare view</a></li>
</ul>
</details>
<br />

Updates `docker/metadata-action` from 6.0.0 to 6.1.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/metadata-action/releases">docker/metadata-action's releases</a>.</em></p>
<blockquote>
<h2>v6.1.0</h2>
<ul>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.79.0 to 0.90.0 in <a href="">docker/metadata-action#613</a></li>
<li>Bump brace-expansion from 1.1.12 to 5.0.6 in <a href="">docker/metadata-action#658</a> <a href="">docker/metadata-action#630</a></li>
<li>Bump csv-parse from 6.1.0 to 6.2.1 in <a href="">docker/metadata-action#617</a></li>
<li>Bump fast-xml-parser from 5.4.2 to 5.8.0 in <a href="">docker/metadata-action#620</a></li>
<li>Bump flatted from 3.3.3 to 3.4.2 in <a href="">docker/metadata-action#623</a></li>
<li>Bump glob from 10.3.15 to 10.5.0 in <a href="">docker/metadata-action#621</a></li>
<li>Bump handlebars from 4.7.8 to 4.7.9 in <a href="">docker/metadata-action#629</a></li>
<li>Bump lodash from 4.17.23 to 4.18.1 in <a href="">docker/metadata-action#639</a></li>
<li>Bump moment-timezone from 0.6.0 to 0.6.1 in <a href="">docker/metadata-action#619</a></li>
<li>Bump picomatch from 4.0.3 to 4.0.4 in <a href="">docker/metadata-action#626</a></li>
<li>Bump postcss from 8.5.6 to 8.5.10 in <a href="">docker/metadata-action#649</a></li>
<li>Bump tar from 6.2.1 to 7.5.15 in <a href="">docker/metadata-action#657</a></li>
<li>Bump undici from 6.23.0 to 6.25.0 in <a href="">docker/metadata-action#614</a></li>
<li>Bump vite from 7.3.1 to 7.3.2 in <a href="">docker/metadata-action#637</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/metadata-action/compare/v6.0.0...v6.1.0">https://github.com/docker/metadata-action/compare/v6.0.0...v6.1.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>80c7e94</code></a> Merge pull request <a href="">#613</a> from docker/dependabot/npm_and_yarn/docker/actions-to...</li>
<li><a href=""><code>8e0ddab</code></a> chore: update generated content</li>
<li><a href=""><code>a8db14b</code></a> chore(deps): Bump <code>@​docker/actions-toolkit</code> from 0.79.0 to 0.90.0</li>
<li><a href=""><code>63a7371</code></a> Merge pull request <a href="">#617</a> from docker/dependabot/npm_and_yarn/csv-parse-6.2.0</li>
<li><a href=""><code>c6916a6</code></a> chore: update generated content</li>
<li><a href=""><code>aca9205</code></a> chore(deps): Bump csv-parse from 6.1.0 to 6.2.1</li>
<li><a href=""><code>9dcfe60</code></a> Merge pull request <a href="">#629</a> from docker/dependabot/npm_and_yarn/handlebars-4.7.9</li>
<li><a href=""><code>43dea76</code></a> chore: update generated content</li>
<li><a href=""><code>7a56f5a</code></a> chore(deps): Bump handlebars from 4.7.8 to 4.7.9</li>
<li><a href=""><code>e49e0aa</code></a> Merge pull request <a href="">#658</a> from docker/dependabot/npm_and_yarn/brace-expansion-5...</li>
<li>Additional commits viewable in <a href="https://github.com/docker/metadata-action/compare/030e881283bb7a6894de51c315a6bfe6a94e05cf...80c7e94dd9b9319bd5eb7a0e0fe9291e23a2a2e9">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d35184bf2063`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.