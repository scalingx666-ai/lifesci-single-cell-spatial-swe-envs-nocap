# Issue

**Title:** [DEPENDABOT]: Bump actions/checkout from 3.0.2 to 4.1.2

## Description

Bumps [actions/checkout](https://github.com/actions/checkout) from 3.0.2 to 4.1.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/releases">actions/checkout's releases</a>.</em></p>
<blockquote>
<h2>v4.1.2</h2>
<p>We are investigating the following issue with this release and have rolled-back the <code>v4</code> tag to point to <code>v4.1.1</code></p>
<ul>
<li><code>sparse-checkout</code> is not available on git versions prior to 2.27.0 (see <a href="">actions/checkout#1651</a>)</li>
</ul>
<h2>What's Changed</h2>
<ul>
<li>Fix: Disable sparse checkout whenever <code>sparse-checkout</code> option is not present <a href="https://github.com/dscho"><code>@​dscho</code></a> in <a href="">actions/checkout#1598</a></li>
<li>Bump tough-cookie from 4.0.0 to 4.1.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/checkout#1406</a></li>
<li>Bump <code>@​babel/traverse</code> from 7.20.5 to 7.24.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/checkout#1642</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/jww3"><code>@​jww3</code></a> made their first contribution in <a href="">actions/checkout#1616</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v4.1.1...v4.1.2">https://github.com/actions/checkout/compare/v4.1.1...v4.1.2</a></p>
<h2>v4.1.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Update CODEOWNERS to Launch team by <a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> in <a href="">actions/checkout#1510</a></li>
<li>Correct link to GitHub Docs by <a href="https://github.com/peterbe"><code>@​peterbe</code></a> in <a href="">actions/checkout#1511</a></li>
<li>Link to release page from what's new section by <a href="https://github.com/cory-miller"><code>@​cory-miller</code></a> in <a href="">actions/checkout#1514</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> made their first contribution in <a href="">actions/checkout#1510</a></li>
<li><a href="https://github.com/peterbe"><code>@​peterbe</code></a> made their first contribution in <a href="">actions/checkout#1511</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v4.1.0...v4.1.1">https://github.com/actions/checkout/compare/v4.1.0...v4.1.1</a></p>
<h2>v4.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update README.md for V4 by <a href="https://github.com/sivapalan"><code>@​sivapalan</code></a> in <a href="">actions/checkout#1452</a></li>
<li>Add support for partial checkout filters by <a href="https://github.com/finleygn"><code>@​finleygn</code></a> in <a href="">actions/checkout#1396</a></li>
<li>Prepare 4.1.0 release by <a href="https://github.com/cory-miller"><code>@​cory-miller</code></a> in <a href="">actions/checkout#1496</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/sivapalan"><code>@​sivapalan</code></a> made their first contribution in <a href="">actions/checkout#1452</a></li>
<li><a href="https://github.com/finleygn"><code>@​finleygn</code></a> made their first contribution in <a href="">actions/checkout#1396</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v4.0.0...v4.1.0">https://github.com/actions/checkout/compare/v4.0.0...v4.1.0</a></p>
<h2>v4.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update default runtime to node20 by <a href="https://github.com/takost"><code>@​takost</code></a> in <a href="">actions/checkout#1436</a></li>
<li>Support fetching without the --progress option by <a href="https://github.com/simonbaird"><code>@​simonbaird</code></a> in <a href="">actions/checkout#1067</a></li>
<li>Release 4.0.0 by <a href="https://github.com/takost"><code>@​takost</code></a> in <a href="">actions/checkout#1447</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/takost"><code>@​takost</code></a> made their first contribution in <a href="">actions/checkout#1436</a></li>
<li><a href="https://github.com/simonbaird"><code>@​simonbaird</code></a> made their first contribution in <a href="">actions/checkout#1067</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v3...v4.0.0">https://github.com/actions/checkout/compare/v3...v4.0.0</a></p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/blob/main/CHANGELOG.md">actions/checkout's changelog</a>.</em></p>
<blockquote>
<h2>v4.1.2</h2>
<ul>
<li>Fix: Disable sparse checkout whenever <code>sparse-checkout</code> option is not present <a href="https://github.com/dscho"><code>@​dscho</code></a> in <a href="">actions/checkout#1598</a></li>
</ul>
<h2>v4.1.1</h2>
<ul>
<li>Correct link to GitHub Docs by <a href="https://github.com/peterbe"><code>@​peterbe</code></a> in <a href="">actions/checkout#1511</a></li>
<li>Link to release page from what's new section by <a href="https://github.com/cory-miller"><code>@​cory-miller</code></a> in <a href="">actions/checkout#1514</a></li>
</ul>
<h2>v4.1.0</h2>
<ul>
<li><a href="">Add support for partial checkout filters</a></li>
</ul>
<h2>v4.0.0</h2>
<ul>
<li><a href="">Support fetching without the --progress option</a></li>
<li><a href="">Update to node20</a></li>
</ul>
<h2>v3.6.0</h2>
<ul>
<li><a href="">Fix: Mark test scripts with Bash'isms to be run via Bash</a></li>
<li><a href="">Add option to fetch tags even if fetch-depth &gt; 0</a></li>
</ul>
<h2>v3.5.3</h2>
<ul>
<li><a href="">Fix: Checkout fail in self-hosted runners when faulty submodule are checked-in</a></li>
<li><a href="">Fix typos found by codespell</a></li>
<li><a href="">Add support for sparse checkouts</a></li>
</ul>
<h2>v3.5.2</h2>
<ul>
<li><a href="">Fix api endpoint for GHES</a></li>
</ul>
<h2>v3.5.1</h2>
<ul>
<li><a href="">Fix slow checkout on Windows</a></li>
</ul>
<h2>v3.5.0</h2>
<ul>
<li><a href="">Add new public key for known_hosts</a></li>
</ul>
<h2>v3.4.0</h2>
<ul>
<li><a href="">Upgrade codeql actions to v2</a></li>
<li><a href="">Upgrade dependencies</a></li>
<li><a href="">Upgrade <code>@​actions/io</code></a></li>
</ul>
<h2>v3.3.0</h2>
<ul>
<li><a href="">Implement branch list using callbacks from exec function</a></li>
<li><a href="">Add in explicit reference to private checkout options</a></li>
<li>[Fix comment typos (that got added in <a href="">#770</a>)](<a href="">actions/checkout#1057</a>)</li>
</ul>
<h2>v3.2.0</h2>
<ul>
<li><a href="">Add GitHub Action to perform release</a></li>
<li><a href="">Fix status badge</a></li>
<li><a href="">Replace datadog/squid with ubuntu/squid Docker image</a></li>
<li><a href="">Wrap pipeline commands for submoduleForeach in quotes</a></li>
<li><a href="">Update <code>@​actions/io</code> to 1.1.2</a></li>
<li><a href="">Upgrading version to 3.2.0</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9bb5618</code></a> Prep for release of  v4.1.2  (<a href="">#1649</a>)</li>
<li><a href=""><code>8eb1f6a</code></a> Bump <code>@​babel/traverse</code> from 7.20.5 to 7.24.0 (<a href="">#1642</a>)</li>
<li><a href=""><code>556e4c3</code></a> Bump tough-cookie from 4.0.0 to 4.1.3 (<a href="">#1406</a>)</li>
<li><a href=""><code>b32f140</code></a> Warn on attempts to publish <code>test-ubuntu-git</code> from non-main branch. (<a href="">#1623</a>)</li>
<li><a href=""><code>2650dbd</code></a> Give <code>test-ubuntu-git</code> its own <code>README</code> (<a href="">#1620</a>)</li>
<li><a href=""><code>aadec89</code></a> Explicitly disable sparse checkout unless asked for (<a href="">#1598</a>)</li>
<li><a href=""><code>df0bcdd</code></a> Refine workflow for generating <code>test-ubuntu-git</code> (<a href="">#1617</a>)</li>
<li><a href=""><code>473055b</code></a> Create <code>test-ubuntu-git</code> Docker Container for Proxy Tests (<a href="">#1616</a>)</li>
<li><a href=""><code>b4ffde6</code></a> Link to release page from what's new section (<a href="">#1514</a>)</li>
<li><a href=""><code>8530928</code></a> Correct link to GitHub Docs (<a href="">#1511</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/checkout/compare/v3.0.2...v4.1.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/checkout&package-manager=github_actions&previous-version=3.0.2&new-version=4.1.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dbf4b7cec1ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.