# Issue

**Title:** chore(deps): bump svgo from 4.0.2 to 4.1.0 in /website

## Description

Bumps [svgo](https://github.com/svg/svgo) from 4.0.2 to 4.1.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/svg/svgo/releases">svgo's releases</a>.</em></p>
<blockquote>
<h2>v4.1.0</h2>
<p>This minor release upgrades the SAX parser and introduces stricter XML validation. It also includes important security hardening for <code>removeScripts</code>, dependency updates, and improvements to the test and regression infrastructure.</p>
<h3>Support SVGO</h3>
<p>If SVGO is valuable to you or your organization, please consider <a href="https://opencollective.com/svgo">supporting the project on OpenCollective</a>. Your sponsorship helps fund ongoing maintenance and security work.</p>
<h3>Stricter XML validation</h3>
<p>SVGO now uses <a href="https://www.npmjs.com/package/sax"><code>sax</code> 1.6.1</a>, upgraded from 1.5.0 (<a href="">#2257</a>).</p>
<p>The new parser version validates numeric character references against the ranges permitted by XML. Invalid references are now rejected in both text and attributes, including:</p>
<ul>
<li>disallowed control characters such as <code>&amp;;</code>, <code>&amp;#xB;</code>, and <code>&amp;#x1F;</code>;</li>
<li>UTF-16 surrogate code points such as <code>&amp;#xD800;</code>;</li>
<li>invalid XML code points such as <code>&amp;#xFFFF;</code>.</li>
</ul>
<p>Valid boundary values—including <code>U+0020</code>, <code>U+D7FF</code>, <code>U+E000</code>, <code>U+FFFD</code>, and characters through <code>U+10FFFF</code>—remain supported.</p>
<p>Parser failures are consistently exposed as <code>SvgoParserError</code> errors with an <code>Invalid character entity</code> reason.</p>
<p>This is an intentional behavior change: malformed SVGs that were previously accepted may now produce a parser error, while valid XML documents are unaffected.</p>
<h3>Security</h3>
<p>The <a href="https://svgo.dev/docs/plugins/removeScripts/"><code>removeScripts</code></a> plugin has been hardened against several script-execution bypasses:</p>
<ul>
<li>Filters executable <code>data:</code> URLs containing HTML, XHTML, or SVG documents while preserving inert data such as PNG images, and filters legacy <code>vbscript:</code> URLs (<a href="">#2263</a>).</li>
<li>Sanitizes content inside SVG <code>&lt;foreignObject&gt;</code> elements by removing HTML event-handler attributes, <code>srcdoc</code>, and executable URLs from <code>action</code>, <code>data</code>, <code>formaction</code>, <code>href</code>, and <code>src</code>, while preserving non-executable HTML and visual content (<a href="">#2264</a>).</li>
<li>Recognizes namespace-prefixed SVG <code>&lt;a&gt;</code> elements and removes ASCII tabs and newlines before checking URL schemes, preventing values such as <code>java&amp;;script:</code> from bypassing detection while preserving elements in unrelated custom namespaces (<a href="">#2268</a>).</li>
</ul>
<p>These changes address:</p>
<ul>
<li><a href="https://github.com/svg/svgo/security/advisories/GHSA-4vpr-x523-8j87">GHSA-4vpr-x523-8j87</a></li>
<li><a href="https://github.com/svg/svgo/security/advisories/GHSA-w27v-7q3p-w38r">GHSA-w27v-7q3p-w38r</a></li>
</ul>
<h3>Dependencies</h3>
<ul>
<li>Upgraded <code>css-select</code> to v6 and <code>css-what</code> to v7, and updated SVGO's custom selector adapter for <code>css-select</code> v6 (<a href="">#2244</a>).</li>
</ul>
<h3>Project maintenance</h3>
<p><a href="https://github.com/TrySound"><code>@​TrySound</code></a> is back as an active SVGO maintainer.</p>
<p>Many thanks to <a href="https://github.com/KTibow"><code>@​KTibow</code></a>, <a href="https://github.com/SethFalco"><code>@​SethFalco</code></a>, and <a href="https://github.com/XhmikosR"><code>@​XhmikosR</code></a> for maintaining and improving SVGO over the past several years.</p>
<p><strong>Full Changelog:</strong> <a href="https://github.com/svg/svgo/compare/v4.0.2...v4.1.0">https://github.com/svg/svgo/compare/v4.0.2...v4.1.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5765cbe</code></a> chore: prepare v4.1.0 release (<a href="">#2275</a>)</li>
<li><a href=""><code>3db3ef3</code></a> fix(removeScripts): handle anchor URL bypasses (<a href="">#2268</a>)</li>
<li><a href=""><code>4e9b9ae</code></a> chore: cache regression screenshots (<a href="">#2267</a>)</li>
<li><a href=""><code>d55270c</code></a> chore(regression): migrate comparison workers to Tinypool (<a href="">#2266</a>)</li>
<li><a href=""><code>fd51e47</code></a> fix(removeScripts): sanitize foreignObject content (<a href="">#2264</a>)</li>
<li><a href=""><code>dcaf957</code></a> chore: optimize fixtures in a bounded worker pool (<a href="">#2265</a>)</li>
<li><a href=""><code>a354293</code></a> fix(removeScripts): filter executable data URLs (<a href="">#2263</a>)</li>
<li><a href=""><code>4e0d2ac</code></a> ci(typecheck): return typechecking on CI</li>
<li><a href=""><code>0b97fed</code></a> test(typescript): drop tsd for vitest type testing API</li>
<li><a href=""><code>f6e8ae1</code></a> chore(pnpm): drop package.json#pnpm.onlyBuiltDependencies</li>
<li>Additional commits viewable in <a href="https://github.com/svg/svgo/compare/v4.0.2...v4.1.0">compare view</a></li>
</ul>
</details>
<details>
<summary>Maintainer changes</summary>
<p>This version was pushed to npm by <a href="https://www.npmjs.com/~GitHub%20Actions">GitHub Actions</a>, a new releaser for svgo since your current version.</p>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=svgo&package-manager=npm_and_yarn&previous-version=4.0.2&new-version=4.1.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3be8b31d312`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.