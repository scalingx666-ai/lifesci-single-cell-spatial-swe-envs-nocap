# Issue

**Title:** chore(deps): bump postcss-selector-parser from 6.1.4 to 6.1.5 in /website

## Description

Bumps [postcss-selector-parser](https://github.com/postcss/postcss-selector-parser) from 6.1.4 to 6.1.5.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/postcss/postcss-selector-parser/releases">postcss-selector-parser's releases</a>.</em></p>
<blockquote>
<h2>6.1.5</h2>
<ul>
<li>fix: parse flat selectors in linear time, closing a CPU exhaustion vulnerability (<a href="https://github.com/advisories/GHSA-rj75-hqrm-r3gf">CVE-2026-104844</a> / GHSA-rj75-hqrm-r3gf, reported by Wayde Shi), backported from 7.1.6 (<a href="">#346</a> by <a href="https://github.com/bradyshutt"><code>@​bradyshutt</code></a>)</li>
</ul>
<h3>The 6.x line is now in security-only maintenance</h3>
<p>This release exists because the advisory above covers every published 6.x
version, and until now the only remediation on offer was an upgrade to 7.x.
<strong>6.1.5 is the patched version for the 6.x line.</strong></p>
<p>The line is kept alive for the installed base that cannot move to 7 yet, Tailwind
CSS 3 in particular, which depends on <code>^6.1.2</code>. From here on it receives security
fixes only: no features, no other bug fixes, no type changes. Everything else
goes to 7.x, where this package is actively developed. Tailwind CSS 4 no longer
depends on this package at all, so this line is expected to retire on its own.</p>
<p>6.1.5 is published under the <code>legacy-v6</code> npm dist-tag, so
<code>npm install postcss-selector-parser</code> keeps resolving to 7.x. Existing <code>^6</code>
ranges pick up 6.1.5 as usual.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/postcss/postcss-selector-parser/blob/6.1.5/CHANGELOG.md">postcss-selector-parser's changelog</a>.</em></p>
<blockquote>
<h1>6.1.5 - 2026-10-19</h1>
<ul>
<li>fix: parse flat selectors in linear time, closing a CPU exhaustion vulnerability (<a href="https://github.com/advisories/GHSA-rj75-hqrm-r3gf">CVE-2026-104844</a> / GHSA-rj75-hqrm-r3gf, reported by Wayde Shi), backported from 7.1.6 (<a href="">#346</a> by <a href="https://github.com/bradyshutt"><code>@​bradyshutt</code></a>)</li>
</ul>
<h3>The 6.x line is now in security-only maintenance</h3>
<p>This release exists because the advisory above covers every published 6.x
version, and until now the only remediation on offer was an upgrade to 7.x.
<strong>6.1.5 is the patched version for the 6.x line.</strong></p>
<p>The line is kept alive for the installed base that cannot move to 7 yet, Tailwind
CSS 3 in particular, which depends on <code>^6.1.2</code>. From here on it receives security
fixes only: no features, no other bug fixes, no type changes. Everything else
goes to 7.x, where this package is actively developed. Tailwind CSS 4 no longer
depends on this package at all, so this line is expected to retire on its own.</p>
<p>6.1.5 is published under the <code>legacy-v6</code> npm dist-tag, so
<code>npm install postcss-selector-parser</code> keeps resolving to 7.x. Existing <code>^6</code>
ranges pick up 6.1.5 as usual.</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d90b6e3</code></a> 6.1.5</li>
<li><a href=""><code>70b0779</code></a> fix: parse flat selectors in linear time, closing a CPU exhaustion vulnerabil...</li>
<li><a href=""><code>fb22e12</code></a> 6.1.4</li>
<li><a href=""><code>99d9299</code></a> fix: tolerate non-node children when serializing selectors</li>
<li><a href=""><code>08ac3e5</code></a> 6.1.3</li>
<li><a href=""><code>bd927e2</code></a> npm audit fix + update CI</li>
<li><a href=""><code>b6330e5</code></a> Improve fix CVE-2026-9358 (NVD) / SNYK-JS-POSTCSSSELECTORPARSER-16873882 (clo...</li>
<li><a href=""><code>053e949</code></a> Fix CVE-2026-9358 (NVD) / SNYK-JS-POSTCSSSELECTORPARSER-16873882 (<a href="">#316</a>)</li>
<li><a href=""><code>0b773f1</code></a> fix: improve typings of constructor helpers (<a href="">#292</a>)</li>
<li><a href=""><code>29843e3</code></a> chore(deps-dev): bump braces from 3.0.2 to 3.0.3 (<a href="">#291</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/postcss/postcss-selector-parser/compare/6.1.4...6.1.5">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=postcss-selector-parser&package-manager=npm_and_yarn&previous-version=6.1.4&new-version=6.1.5)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/COMBINE-lab/salmon/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e461104506f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.