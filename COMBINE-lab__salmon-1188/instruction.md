# Issue

**Title:** chore(deps): bump the website-minor group in /website with 2 updates

## Description

Bumps the website-minor group in /website with 2 updates: [@astrojs/starlight](https://github.com/withastro/starlight/tree/HEAD/packages/starlight) and [astro](https://github.com/withastro/astro/tree/HEAD/packages/astro).

Updates `@astrojs/starlight` from 0.41.4 to 0.41.7
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/withastro/starlight/releases">@​astrojs/starlight's releases</a>.</em></p>
<blockquote>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.41.7</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4114</a> <a href=""><code>3e486fb</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Fixes processing of code examples in RTL languages when using Astro’s Sätteri Markdown processor</li>
</ul>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.41.6</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4102</a> <a href=""><code>f1dddc0</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Adds 1 new icon: <code>forgejo</code></li>
</ul>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.41.5</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4095</a> <a href=""><code>bb06434</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Fixes a regression when using a union to <a href="https://starlight.astro.build/reference/frontmatter/#extend">extend</a> Starlight’s <code>docsSchema()</code>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/withastro/starlight/blob/main/packages/starlight/CHANGELOG.md">@​astrojs/starlight's changelog</a>.</em></p>
<blockquote>
<h2>0.41.7</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4114</a> <a href=""><code>3e486fb</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Fixes processing of code examples in RTL languages when using Astro’s Sätteri Markdown processor</li>
</ul>
<h2>0.41.6</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4102</a> <a href=""><code>f1dddc0</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Adds 1 new icon: <code>forgejo</code></li>
</ul>
<h2>0.41.5</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4095</a> <a href=""><code>bb06434</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Fixes a regression when using a union to <a href="https://starlight.astro.build/reference/frontmatter/#extend">extend</a> Starlight’s <code>docsSchema()</code>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>656ffd5</code></a> [ci] release (<a href="">#4115</a>)</li>
<li><a href=""><code>612fd0a</code></a> Update dependencies (<a href="">#4113</a>)</li>
<li><a href=""><code>3e486fb</code></a> Refactor Sätteri RTL code support plugin (<a href="">#4114</a>)</li>
<li><a href=""><code>ae0838f</code></a> [ci] release (<a href="">#4106</a>)</li>
<li><a href=""><code>f1dddc0</code></a> Add Forgejo icon (<a href="">#4102</a>)</li>
<li><a href=""><code>5b06909</code></a> [ci] release (<a href="">#4097</a>)</li>
<li><a href=""><code>bb06434</code></a> Fix union schema <code>extend</code> regression (<a href="">#4095</a>)</li>
<li>See full diff in <a href="https://github.com/withastro/starlight/commits/@astrojs/starlight@0.41.7/packages/starlight">compare view</a></li>
</ul>
</details>
<br />

Updates `astro` from 7.1.3 to 7.2.4
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/withastro/astro/releases">astro's releases</a>.</em></p>
<blockquote>
<h2>astro@7.2.4</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17747</a> <a href=""><code>a90ff66</code></a> Thanks <a href="https://github.com/Princesseuh"><code>@​Princesseuh</code></a>! - Fixes builds hanging when an image file is malformed</p>
</li>
<li>
<p><a href="">#17701</a> <a href=""><code>05763a0</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes base path stripping to respect path-segment boundaries. With a configured <code>base</code> such as <code>/docs</code>, a request like <code>/docs-archive/page</code> is no longer treated as being under the base, so routing and <code>context.url.pathname</code> now agree on the same pathname.</p>
</li>
<li>
<p><a href="">#17742</a> <a href=""><code>70b449d</code></a> Thanks <a href="https://github.com/Kjubikstronk"><code>@​Kjubikstronk</code></a>! - Fixes <code>astro build</code> throwing <code>TypeError: Missing parameter</code> for dynamic routes when <code>build.format: 'preserve'</code> and <code>trailingSlash: 'always'</code> are used together. Stripping the framework-injected <code>.html</code> suffix dropped the trailing slash that the compiled route pattern requires, so the route no longer matched itself and its params resolved as empty.</p>
</li>
<li>
<p><a href="">#17703</a> <a href=""><code>771b0a9</code></a> Thanks <a href="https://github.com/astrobot-houston"><code>@​astrobot-houston</code></a>! - Fixes <code>Astro.site</code> always being <code>undefined</code> when rendering components via the Container API, even when <code>site</code> is set in <code>astroConfig</code></p>
</li>
<li>
<p>Updated dependencies [<a href=""><code>05763a0</code></a>, <a href=""><code>bc171af</code></a>]:</p>
<ul>
<li><code>@​astrojs/internal-helpers</code><a href="https://github.com/0"><code>@​0</code></a>.10.4</li>
<li><code>@​astrojs/markdown-satteri</code><a href="https://github.com/0"><code>@​0</code></a>.3.7</li>
<li><code>@​astrojs/markdown-remark</code><a href="https://github.com/7"><code>@​7</code></a>.2.4</li>
</ul>
</li>
</ul>
<h2>astro@7.2.3</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17724</a> <a href=""><code>97140b2</code></a> Thanks <a href="https://github.com/ematipico"><code>@​ematipico</code></a>! - Fixes an issue where Astro could run out of memory when <code>experimental.collectionStorage</code> is set to <code>chunked</code> and there are multiple concurrent updates to the same collection.</p>
</li>
<li>
<p><a href="">#17636</a> <a href=""><code>51723b1</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes the dev server sometimes matching against stale routes after pages were added, removed, or renamed, requiring a dev server restart to pick up the change</p>
</li>
<li>
<p><a href="">#17636</a> <a href=""><code>51723b1</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes the composable request helpers (<code>astro/fetch</code>) throwing an error when used on a request that had been rewritten with <code>Astro.rewrite()</code> or <code>next()</code></p>
</li>
<li>
<p><a href="">#17636</a> <a href=""><code>51723b1</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Refactors Astro's internal server-side request handling. This is an internal change: all documented public APIs, including <code>App</code> and <code>NodeApp</code>, keep their existing signatures and behavior.</p>
<p>The undocumented internal <code>app.pipeline</code> property and the <code>AppPipeline</code> export from <code>astro/app</code> have been removed. Adapters that used <code>app.pipeline.getLogger()</code> to wait for the configured log destination can call the new <code>app.getLogger()</code> instead.</p>
<p>As a result of this refactor, <code>new FetchState(request)</code> from <code>astro/fetch</code> now works anywhere inside a built Astro server — including custom <code>src/fetch.ts</code> entrypoints — without the request needing to first pass through <code>app.render()</code>. Previously this threw an error, breaking patterns like the Cloudflare adapter's advanced custom-worker setup.</p>
</li>
<li>
<p><a href="">#17723</a> <a href=""><code>c3b9aed</code></a> Thanks <a href="https://github.com/florian-lefebvre"><code>@​florian-lefebvre</code></a>! - Fixes a link in font providers JSDoc annotations</p>
</li>
<li>
<p><a href="">#17699</a> <a href=""><code>e28d227</code></a> Thanks <a href="https://github.com/ArmandPhilippot"><code>@​ArmandPhilippot</code></a>! - Fixes several documentation issues related to the JSDoc for configuration options.</p>
<ul>
<li>When hovering over the <code>server</code> and <code>fonts</code> options, the JSDoc for the nested options was displayed instead of the JSDoc for the top-level property.</li>
<li>Two i18n configuration options were being used incorrectly in the examples.</li>
<li>The indentation of some code blocks was broken on hover.</li>
</ul>
</li>
<li>
<p><a href="">#17572</a> <a href=""><code>2066f39</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes a crash when a request arrives with a malformed port in the <code>Host</code> header (for example <code>example.com:65536</code> or <code>example.com:8080:8080</code>). Such a host made the constructed request URL invalid, and the fallback that was meant to recover reused the same invalid host and threw again. The request URL now degrades to a host the server controls when the incoming host cannot be parsed, so the request is handled instead of erroring.</p>
</li>
<li>
<p><a href="">#17685</a> <a href=""><code>9f15609</code></a> Thanks <a href="https://github.com/astrobot-houston"><code>@​astrobot-houston</code></a>! - Fixes a dev server error where an SSR full reload triggered by a third-party Vite plugin (such as <code>@tailwindcss/vite</code>) could fail with <code>Failed to load url astro:server-app.js</code></p>
</li>
<li>
<p><a href="">#17636</a> <a href=""><code>51723b1</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Improves error handling for custom log destinations. When the configured logger fails to load, Astro now reports the error and continues with the default console logger instead of failing the first request.</p>
</li>
<li>
<p><a href="">#17631</a> <a href=""><code>cf29bec</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes <code>getCollection()</code> and <code>getEntry()</code> throwing <code>DataCloneError</code> when a collection schema transform returns a <code>Temporal.PlainDate</code> or other class instance.</p>
</li>
<li>
<p>Updated dependencies [<a href=""><code>8c193f6</code></a>]:</p>
<ul>
<li><code>@​astrojs/internal-helpers</code><a href="https://github.com/0"><code>@​0</code></a>.10.3</li>
<li><code>@​astrojs/markdown-remark</code><a href="https://github.com/7"><code>@​7</code></a>.2.3</li>
</ul>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/withastro/astro/blob/main/packages/astro/CHANGELOG.md">astro's changelog</a>.</em></p>
<blockquote>
<h2>7.2.4</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17747</a> <a href=""><code>a90ff66</code></a> Thanks <a href="https://github.com/Princesseuh"><code>@​Princesseuh</code></a>! - Fixes builds hanging when an image file is malformed</p>
</li>
<li>
<p><a href="">#17701</a> <a href=""><code>05763a0</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes base path stripping to respect path-segment boundaries. With a configured <code>base</code> such as <code>/docs</code>, a request like <code>/docs-archive/page</code> is no longer treated as being under the base, so routing and <code>context.url.pathname</code> now agree on the same pathname.</p>
</li>
<li>
<p><a href="">#17742</a> <a href=""><code>70b449d</code></a> Thanks <a href="https://github.com/Kjubikstronk"><code>@​Kjubikstronk</code></a>! - Fixes <code>astro build</code> throwing <code>TypeError: Missing parameter</code> for dynamic routes when <code>build.format: 'preserve'</code> and <code>trailingSlash: 'always'</code> are used together. Stripping the framework-injected <code>.html</code> suffix dropped the trailing slash that the compiled route pattern requires, so the route no longer matched itself and its params resolved as empty.</p>
</li>
<li>
<p><a href="">#17703</a> <a href=""><code>771b0a9</code></a> Thanks <a href="https://github.com/astrobot-houston"><code>@​astrobot-houston</code></a>! - Fixes <code>Astro.site</code> always being <code>undefined</code> when rendering components via the Container API, even when <code>site</code> is set in <code>astroConfig</code></p>
</li>
<li>
<p>Updated dependencies [<a href=""><code>05763a0</code></a>, <a href=""><code>bc171af</code></a>]:</p>
<ul>
<li><code>@​astrojs/internal-helpers</code><a href="https://github.com/0"><code>@​0</code></a>.10.4</li>
<li><code>@​astrojs/markdown-satteri</code><a href="https://github.com/0"><code>@​0</code></a>.3.7</li>
<li><code>@​astrojs/markdown-remark</code><a href="https://github.com/7"><code>@​7</code></a>.2.4</li>
</ul>
</li>
</ul>
<h2>7.2.3</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17724</a> <a href=""><code>97140b2</code></a> Thanks <a href="https://github.com/ematipico"><code>@​ematipico</code></a>! - Fixes an issue where Astro could run out of memory when <code>experimental.collectionStorage</code> is set to <code>chunked</code> and there are multiple concurrent updates to the same collection.</p>
</li>
<li>
<p><a href="">#17636</a> <a href=""><code>51723b1</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes the dev server sometimes matching against stale routes after pages were added, removed, or renamed, requiring a dev server restart to pick up the change</p>
</li>
<li>
<p><a href="">#17636</a> <a href=""><code>51723b1</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes the composable request helpers (<code>astro/fetch</code>) throwing an error when used on a request that had been rewritten with <code>Astro.rewrite()</code> or <code>next()</code></p>
</li>
<li>
<p><a href="">#17636</a> <a href=""><code>51723b1</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Refactors Astro's internal server-side request handling. This is an internal change: all documented public APIs, including <code>App</code> and <code>NodeApp</code>, keep their existing signatures and behavior.</p>
<p>The undocumented internal <code>app.pipeline</code> property and the <code>AppPipeline</code> export from <code>astro/app</code> have been removed. Adapters that used <code>app.pipeline.getLogger()</code> to wait for the configured log destination can call the new <code>app.getLogger()</code> instead.</p>
<p>As a result of this refactor, <code>new FetchState(request)</code> from <code>astro/fetch</code> now works anywhere inside a built Astro server — including custom <code>src/fetch.ts</code> entrypoints — without the request needing to first pass through <code>app.render()</code>. Previously this threw an error, breaking patterns like the Cloudflare adapter's advanced custom-worker setup.</p>
</li>
<li>
<p><a href="">#17723</a> <a href=""><code>c3b9aed</code></a> Thanks <a href="https://github.com/florian-lefebvre"><code>@​florian-lefebvre</code></a>! - Fixes a link in font providers JSDoc annotations</p>
</li>
<li>
<p><a href="">#17699</a> <a href=""><code>e28d227</code></a> Thanks <a href="https://github.com/ArmandPhilippot"><code>@​ArmandPhilippot</code></a>! - Fixes several documentation issues related to the JSDoc for configuration options.</p>
<ul>
<li>When hovering over the <code>server</code> and <code>fonts</code> options, the JSDoc for the nested options was displayed instead of the JSDoc for the top-level property.</li>
<li>Two i18n configuration options were being used incorrectly in the examples.</li>
<li>The indentation of some code blocks was broken on hover.</li>
</ul>
</li>
<li>
<p><a href="">#17572</a> <a href=""><code>2066f39</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes a crash when a request arrives with a malformed port in the <code>Host</code> header (for example <code>example.com:65536</code> or <code>example.com:8080:8080</code>). Such a host made the constructed request URL invalid, and the fallback that was meant to recover reused the same invalid host and threw again. The request URL now degrades to a host the server controls when the incoming host cannot be parsed, so the request is handled instead of erroring.</p>
</li>
<li>
<p><a href="">#17685</a> <a href=""><code>9f15609</code></a> Thanks <a href="https://github.com/astrobot-houston"><code>@​astrobot-houston</code></a>! - Fixes a dev server error where an SSR full reload triggered by a third-party Vite plugin (such as <code>@tailwindcss/vite</code>) could fail with <code>Failed to load url astro:server-app.js</code></p>
</li>
<li>
<p><a href="">#17636</a> <a href=""><code>51723b1</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Improves error handling for custom log destinations. When the configured logger fails to load, Astro now reports the error and continues with the default console logger instead of failing the first request.</p>
</li>
<li>
<p><a href="">#17631</a> <a href=""><code>cf29bec</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes <code>getCollection()</code> and <code>getEntry()</code> throwing <code>DataCloneError</code> when a collection schema transform returns a <code>Temporal.PlainDate</code> or other class instance.</p>
</li>
<li>
<p>Updated dependencies [<a href=""><code>8c193f6</code></a>]:</p>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8a31cba</code></a> [ci] release (<a href="">#17739</a>)</li>
<li><a href=""><code>aeda810</code></a> [ci] format</li>
<li><a href=""><code>a90ff66</code></a> fix(assets): harden vendored image-size box and entry checks (<a href="">#17747</a>)</li>
<li><a href=""><code>05763a0</code></a> Respect path-segment boundaries when stripping the configured base (<a href="">#17701</a>)</li>
<li><a href=""><code>70b449d</code></a> fix(routing): keep the trailing slash when stripping an injected .html (<a href="">#17742</a>)</li>
<li><a href=""><code>771b0a9</code></a> fix(container): wire astroConfig.site through to the SSR manifest so Astro.si...</li>
<li><a href=""><code>52e6c34</code></a> [ci] release (<a href="">#17691</a>)</li>
<li><a href=""><code>97140b2</code></a> fix(collections): chunk writing of collections (<a href="">#17724</a>)</li>
<li><a href=""><code>e28d227</code></a> docs: fix the code snippets in the JSDoc for the configuration options (<a href="">#17699</a>)</li>
<li><a href=""><code>c3b9aed</code></a> chore: remove unifont workaround (<a href="">#17723</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/withastro/astro/commits/astro@7.2.4/packages/astro">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9caef6ee0e4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.