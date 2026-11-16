# Issue

**Title:** chore(deps): bump undici from 8.10.0 to 8.11.2 in /website

## Description

Bumps [undici](https://github.com/nodejs/undici) from 8.10.0 to 8.11.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/nodejs/undici/releases">undici's releases</a>.</em></p>
<blockquote>
<h2>v8.11.2</h2>
<h2>What's Changed</h2>
<ul>
<li>fix: close rejected HTTP/2 WebSocket handshake streams by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#5873</a></li>
<li>fix: avoid reconnecting aborted requests by <a href="https://github.com/Junaid-PK"><code>@​Junaid-PK</code></a> in <a href="">nodejs/undici#5846</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/Junaid-PK"><code>@​Junaid-PK</code></a> made their first contribution in <a href="">nodejs/undici#5846</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/nodejs/undici/compare/v8.11.1...v8.11.2">https://github.com/nodejs/undici/compare/v8.11.1...v8.11.2</a></p>
<h2>v8.11.1</h2>
<h2>What's Changed</h2>
<ul>
<li>deslopify websocket test by <a href="https://github.com/KhafraDev"><code>@​KhafraDev</code></a> in <a href="">nodejs/undici#5851</a></li>
<li>Revert &quot;fix: preserve HTTP/2 for legacy fetch consumers&quot; by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#5860</a></li>
<li>fix websocketstream bugs by <a href="https://github.com/KhafraDev"><code>@​KhafraDev</code></a> in <a href="">nodejs/undici#5863</a></li>
<li>fix hang on 3xx response with large body by <a href="https://github.com/KhafraDev"><code>@​KhafraDev</code></a> in <a href="">nodejs/undici#5850</a></li>
<li>docs: warn about buffering response bodies by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#5872</a></li>
<li>test: cover native fetch gzip decoding through the legacy bridge by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#5874</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/nodejs/undici/compare/v8.11.0...v8.11.1">https://github.com/nodejs/undici/compare/v8.11.0...v8.11.1</a></p>
<h2>v8.11.0</h2>
<h2>What's Changed</h2>
<ul>
<li>fix: complete upgrade diagnostics lifecycle by <a href="https://github.com/BridgeAR"><code>@​BridgeAR</code></a> in <a href="">nodejs/undici#5761</a></li>
<li>build(deps): bump step-security/harden-runner from 2.19.4 to 2.21.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">nodejs/undici#5753</a></li>
<li>fix(decompress): join a repeated content-encoding header by <a href="https://github.com/luantaraschi"><code>@​luantaraschi</code></a> in <a href="">nodejs/undici#5664</a></li>
<li>fix(cookies): keep a cookie named <strong>proto</strong> in getCookies by <a href="https://github.com/luantaraschi"><code>@​luantaraschi</code></a> in <a href="">nodejs/undici#5663</a></li>
<li>build(deps-dev): bump jest from 30.5.0 to 30.5.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">nodejs/undici#5784</a></li>
<li>build(deps): bump got from 15.1.0 to 16.0.0 in /benchmarks by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">nodejs/undici#5785</a></li>
<li>fix: selectively re-enable SIMD for ppc64 by <a href="https://github.com/richardlau"><code>@​richardlau</code></a> in <a href="">nodejs/undici#5776</a></li>
<li>use private fields for brand checks by <a href="https://github.com/KhafraDev"><code>@​KhafraDev</code></a> in <a href="">nodejs/undici#5792</a></li>
<li>fix(h2): do not unref a session with open streams by <a href="https://github.com/kjsik11"><code>@​kjsik11</code></a> in <a href="">nodejs/undici#5782</a></li>
<li>fix(h2): avoid pool fan-out during ALPN negotiation by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#5799</a></li>
<li>fix issue <a href="">#5715</a> by <a href="https://github.com/KhafraDev"><code>@​KhafraDev</code></a> in <a href="">nodejs/undici#5805</a></li>
<li>ci: extend macOS Node.js workflow timeout by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#5775</a></li>
<li>fix(env-http-proxy-agent): NO_PROXY wildcard semantics by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#5777</a></li>
<li>fix(h2): do not replay a request whose response already started after GOAWAY by <a href="https://github.com/kjsik11"><code>@​kjsik11</code></a> in <a href="">nodejs/undici#5788</a></li>
<li>test: skip HTTP/2 churn test on Node.js 25 on all platforms by <a href="https://github.com/kjsik11"><code>@​kjsik11</code></a> in <a href="">nodejs/undici#5790</a></li>
<li>fix(proxy-agent): preserve repeated iterable headers by <a href="https://github.com/GiHoon1123"><code>@​GiHoon1123</code></a> in <a href="">nodejs/undici#5779</a></li>
<li>docs(errors): document ProxyConnectionError (UND_ERR_PRX_CONN) by <a href="https://github.com/kilisamemarisaaa"><code>@​kilisamemarisaaa</code></a> in <a href="">nodejs/undici#5781</a></li>
<li>dataurl parsing improvements + update WPT by <a href="https://github.com/KhafraDev"><code>@​KhafraDev</code></a> in <a href="">nodejs/undici#5812</a></li>
<li>fix(decompress): treat inherited Object.prototype names as unsupported encodings by <a href="https://github.com/NgoQuocViet2001"><code>@​NgoQuocViet2001</code></a> in <a href="">nodejs/undici#5807</a></li>
<li>test(h2): stabilize http2-connection by <a href="https://github.com/ViniciusDev26"><code>@​ViniciusDev26</code></a> in <a href="">nodejs/undici#5801</a></li>
<li>fix: preserve HTTP/2 for non-upgrade legacy requests by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#5811</a></li>
<li>fix: skip drain dispatch for clientTtl-evicted clients in PoolBase by <a href="https://github.com/vwong"><code>@​vwong</code></a> in <a href="">nodejs/undici#5677</a></li>
<li>chore: update tests blocking release by <a href="https://github.com/vwong"><code>@​vwong</code></a> in <a href="">nodejs/undici#5828</a></li>
<li>build(deps): bump uWebSockets.js from v20.68.0 to v20.70.0 in /benchmarks by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">nodejs/undici#5824</a></li>
<li>fix(deduplicate): settle requests when composed with retry by <a href="https://github.com/mcollina"><code>@​mcollina</code></a> in <a href="">nodejs/undici#5817</a></li>
<li>fix(cache): do not report aborted on successful cache hits by <a href="https://github.com/Yahiro025"><code>@​Yahiro025</code></a> in <a href="">nodejs/undici#5819</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7e016ad</code></a> Bumped v8.11.2 (<a href="">#5886</a>)</li>
<li><a href=""><code>fcdd5a6</code></a> fix: skip reconnecting for aborted requests (<a href="">#5846</a>)</li>
<li><a href=""><code>dd28c5c</code></a> fix: close rejected HTTP/2 WebSocket handshake streams (<a href="">#5873</a>)</li>
<li><a href=""><code>5e0a2f8</code></a> Bumped v8.11.1 (<a href="">#5871</a>)</li>
<li><a href=""><code>2b72898</code></a> test: cover native fetch gzip decoding through the legacy bridge (<a href="">#5874</a>)</li>
<li><a href=""><code>636bf51</code></a> docs: warn about buffering response bodies (<a href="">#5872</a>)</li>
<li><a href=""><code>8145595</code></a> fix hang on 3xx response with large body (<a href="">#5850</a>)</li>
<li><a href=""><code>f3cbe48</code></a> fix websocketstream bugs (<a href="">#5863</a>)</li>
<li><a href=""><code>1d4ea0a</code></a> Revert &quot;fix: preserve HTTP/2 for legacy fetch consumers&quot; (<a href="">#5860</a>)</li>
<li><a href=""><code>77d7b3f</code></a> deslopify websocket test (<a href="">#5851</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/nodejs/undici/compare/v8.10.0...v8.11.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=undici&package-manager=npm_and_yarn&previous-version=8.10.0&new-version=8.11.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed926b8f6120`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.