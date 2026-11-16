# Issue

**Title:** chore(deps): bump undici from 8.11.2 to 8.12.3 in /website

## Description

Bumps [undici](https://github.com/nodejs/undici) from 8.11.2 to 8.12.3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/nodejs/undici/releases">undici's releases</a>.</em></p>
<blockquote>
<h2>v8.12.3</h2>
<h2>What's Changed</h2>
<ul>
<li>ci: use Python 3.14 for the WPT server on macOS by <a href="https://github.com/mrityunjay-pandey"><code>@​mrityunjay-pandey</code></a> in <a href="">nodejs/undici#6029</a></li>
<li>build(deps-dev): bump neostandard from 0.13.0 to 0.14.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">nodejs/undici#6006</a></li>
<li>build(deps-dev): bump eslint from 9.39.4 to 10.12.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">nodejs/undici#5967</a></li>
<li>docs: document the options of interceptors.cache() by <a href="https://github.com/qodelicious"><code>@​qodelicious</code></a> in <a href="">nodejs/undici#6050</a></li>
<li>fix(h2): replace a connection that stops responding after a stream timeout by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#6052</a></li>
<li>fix(pool): keep caller async context for queued requests by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#5982</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/qodelicious"><code>@​qodelicious</code></a> made their first contribution in <a href="">nodejs/undici#6050</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/nodejs/undici/compare/v8.12.2...v8.12.3">https://github.com/nodejs/undici/compare/v8.12.2...v8.12.3</a></p>
<h2>v8.12.2</h2>
<h2>Security fixes</h2>
<h3>High severity</h3>
<h4>Denial of service via TLS 1.2 certificate-changing renegotiation</h4>
<p><strong>CVE-2026-87018 · <a href="https://github.com/nodejs/undici/security/advisories/GHSA-qrxm-fqhp-jwvm">GHSA-qrxm-fqhp-jwvm</a></strong></p>
<p>A malicious or compromised HTTPS server could crash the Node.js process by initiating TLS 1.2 renegotiation and presenting a different, CA-trusted certificate whose hostname did not match the requested host. The resulting socket error reached an assertion in undici's HTTP/1.1 and HTTP/2 connection handling. This release handles post-connect certificate errors without terminating the process.</p>
<h4>TLS certificate validation bypass through dropped <code>Agent</code> options</h4>
<p><strong>CVE-2026-109383 · <a href="https://github.com/nodejs/undici/security/advisories/GHSA-2m5v-pch6-74hx">GHSA-2m5v-pch6-74hx</a></strong></p>
<p><code>Agent</code> used a JSON-based clone for constructor options, which silently removed function-valued TLS options such as <code>checkServerIdentity</code>. Applications relying on custom certificate or public-key verification could therefore accept a certificate that the callback was intended to reject. This release preserves TLS options when creating per-origin dispatchers.</p>
<h4>Cache poisoning and cross-user disclosure through cross-origin redirects</h4>
<p><strong>CVE-2026-109829 · <a href="https://github.com/nodejs/undici/security/advisories/GHSA-4w7w-5xrc-9h26">GHSA-4w7w-5xrc-9h26</a></strong></p>
<p>When an originless <code>Agent</code> combined redirect and shared-cache interceptors as <code>compose(redirect(), cache())</code>, a response from a cross-origin redirect could be stored under the original URL. This could allow persistent cache poisoning or disclosure of user-specific responses to later callers. This release verifies the response origin before caching and preserves redirect-hop cache-control policy.</p>
<h4>Denial of service through excessive <code>Content-Encoding</code> values</h4>
<p><strong>CVE-2026-109869 · <a href="https://github.com/nodejs/undici/security/advisories/GHSA-xjj6-f33q-929c">GHSA-xjj6-f33q-929c</a></strong></p>
<p>A malicious HTTP server could crash the Node.js process by returning more than five content codings and closing the connection before sending the body. Although <code>fetch()</code> rejected the response, an error from an orphaned internal stream could remain unhandled. This release validates the content-encoding chain before creating the body stream and aborts oversized chains safely.</p>
<h3>Medium severity</h3>
<h4>Denial of service through the <code>decompress</code> interceptor</h4>
<p><strong>CVE-2026-87029 · <a href="https://github.com/nodejs/undici/security/advisories/GHSA-55wc-3pg8-jfw6">GHSA-55wc-3pg8-jfw6</a></strong></p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ff9cc5e</code></a> Bumped v8.12.3 (<a href="">#6053</a>)</li>
<li><a href=""><code>0bbf614</code></a> fix(pool): keep caller async context for queued requests (<a href="">#5982</a>)</li>
<li><a href=""><code>aa1eef1</code></a> fix(h2): replace a connection that stops responding after a stream timeout (#...</li>
<li><a href=""><code>e34b872</code></a> docs: document the options of interceptors.cache() (<a href="">#6050</a>)</li>
<li><a href=""><code>e8f3423</code></a> build(deps-dev): bump eslint from 9.39.4 to 10.12.0 (<a href="">#5967</a>)</li>
<li><a href=""><code>b777e40</code></a> build(deps-dev): bump neostandard from 0.13.0 to 0.14.0 (<a href="">#6006</a>)</li>
<li><a href=""><code>43700ff</code></a> ci: use Python 3.14 for the WPT server on macOS (<a href="">#6029</a>)</li>
<li><a href=""><code>bb6cc0a</code></a> Bumped v8.12.2 (<a href="">#6021</a>)</li>
<li><a href=""><code>b217373</code></a> fix(websocket): bound automatic PONG writes under backpressure</li>
<li><a href=""><code>789ef26</code></a> fix(eventsource): bound retained SSE parser state</li>
<li>Additional commits viewable in <a href="https://github.com/nodejs/undici/compare/v8.11.2...v8.12.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=undici&package-manager=npm_and_yarn&previous-version=8.11.2&new-version=8.12.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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