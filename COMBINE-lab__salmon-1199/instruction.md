# Issue

**Title:** chore(deps): bump the website-minor group in /website with 3 updates

## Description

Bumps the website-minor group in /website with 3 updates: [@astrojs/starlight](https://github.com/withastro/starlight/tree/HEAD/packages/starlight), [astro](https://github.com/withastro/astro/tree/HEAD/packages/astro) and [sharp](https://github.com/lovell/sharp).

Updates `@astrojs/starlight` from 0.41.7 to 0.41.9
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/withastro/starlight/releases">@​astrojs/starlight's releases</a>.</em></p>
<blockquote>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.41.9</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4145</a> <a href=""><code>1c90d69</code></a> Thanks <a href="https://github.com/pyxelr"><code>@​pyxelr</code></a>! - Adds 1 new icon: <code>goodreads</code></li>
</ul>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.41.8</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#4142</a> <a href=""><code>cacbc9f</code></a> Thanks <a href="https://github.com/alebelcor"><code>@​alebelcor</code></a>! - Adds 1 new icon: <code>whatsApp</code></p>
</li>
<li>
<p><a href="">#4133</a> <a href=""><code>3944311</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Internal refactor: numbered <code>id</code> attributes in the <code>&lt;Tabs&gt;</code> component are now page-specific instead of using a global counter</p>
</li>
<li>
<p><a href="">#4138</a> <a href=""><code>cd4b665</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Fixes localisation of code block UI elements when using the Sätteri Markdown processor</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/withastro/starlight/blob/main/packages/starlight/CHANGELOG.md">@​astrojs/starlight's changelog</a>.</em></p>
<blockquote>
<h2>0.41.9</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4145</a> <a href=""><code>1c90d69</code></a> Thanks <a href="https://github.com/pyxelr"><code>@​pyxelr</code></a>! - Adds 1 new icon: <code>goodreads</code></li>
</ul>
<h2>0.41.8</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#4142</a> <a href=""><code>cacbc9f</code></a> Thanks <a href="https://github.com/alebelcor"><code>@​alebelcor</code></a>! - Adds 1 new icon: <code>whatsApp</code></p>
</li>
<li>
<p><a href="">#4133</a> <a href=""><code>3944311</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Internal refactor: numbered <code>id</code> attributes in the <code>&lt;Tabs&gt;</code> component are now page-specific instead of using a global counter</p>
</li>
<li>
<p><a href="">#4138</a> <a href=""><code>cd4b665</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Fixes localisation of code block UI elements when using the Sätteri Markdown processor</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>bc6b188</code></a> [ci] release (<a href="">#4153</a>)</li>
<li><a href=""><code>1c90d69</code></a> Add Goodreads icon (<a href="">#4145</a>)</li>
<li><a href=""><code>e81fedf</code></a> [ci] release (<a href="">#4137</a>)</li>
<li><a href=""><code>cd4b665</code></a> Fix localisation of Expressive Code UI (<a href="">#4138</a>)</li>
<li><a href=""><code>cacbc9f</code></a> Add WhatsApp icon (<a href="">#4142</a>)</li>
<li><a href=""><code>3944311</code></a> Use a page-specific counter for <code>\&lt;Tabs&gt;</code>  IDs (<a href="">#4133</a>)</li>
<li><a href=""><code>9b8221c</code></a> Remove Vitest native config loader warnings (<a href="">#4129</a>)</li>
<li>See full diff in <a href="https://github.com/withastro/starlight/commits/@astrojs/starlight@0.41.9/packages/starlight">compare view</a></li>
</ul>
</details>
<br />

Updates `astro` from 7.2.4 to 7.2.9
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/withastro/astro/releases">astro's releases</a>.</em></p>
<blockquote>
<h2>astro@7.2.9</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17846</a> <a href=""><code>b441180</code></a> Thanks <a href="https://github.com/Princesseuh"><code>@​Princesseuh</code></a>! - Fixes importing <code>.html</code> files not being typed outside of <code>.astro</code> files</p>
</li>
<li>
<p><a href="">#17831</a> <a href=""><code>32e8b44</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes a crash when requesting <code>/index.html</code> against a dynamic page route like <code>[slug].astro</code></p>
</li>
<li>
<p><a href="">#17841</a> <a href=""><code>c35448e</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes SSR manifest containing stale <code>entryModules</code> references to prerender-only chunks that no longer exist in the final build output</p>
</li>
<li>
<p><a href="">#17847</a> <a href=""><code>eb87a23</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes <code>set:text</code> escaping in MDX script and style elements</p>
</li>
</ul>
<h2>astro@7.2.8</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17837</a> <a href=""><code>ecb4082</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Updates the minimum supported version of Sharp to 0.35.4</p>
</li>
<li>
<p><a href="">#17786</a> <a href=""><code>db7c53b</code></a> Thanks <a href="https://github.com/gameroman"><code>@​gameroman</code></a>! - Replaces the internal <code>find-process</code> dependency with a smaller, lighter alternative</p>
</li>
</ul>
<h2>astro@7.2.7</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17415</a> <a href=""><code>55d38c8</code></a> Thanks <a href="https://github.com/iseraph-dev"><code>@​iseraph-dev</code></a>! - Deserializes each route once when loading the SSR manifest</p>
</li>
<li>
<p><a href="">#17772</a> <a href=""><code>023b48b</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes route selection for normalized request paths in adapter and development request handling</p>
</li>
<li>
<p><a href="">#17819</a> <a href=""><code>633855b</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Updates generated and default Cloudflare <code>compatibility_date</code> values to match the installed runtime and requires Wrangler <code>^4.125.0</code></p>
</li>
<li>
<p><a href="">#17813</a> <a href=""><code>ae26d18</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes <code>rewrite()</code> and <code>next(payload)</code> for GET and HEAD requests with host-provided bodies</p>
</li>
<li>
<p><a href="">#17816</a> <a href=""><code>a0d2fe3</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes the experimental <code>svgOptimizer</code> not generating unique per-file ID prefixes when using SVGO's <code>prefixIds</code> plugin</p>
</li>
</ul>
<h2>astro@7.2.6</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#17812</a> <a href=""><code>29af6da</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes a bug where <code>new FetchState(request)</code> could fail in development when server dependencies were optimized</li>
</ul>
<h2>astro@7.2.5</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17758</a> <a href=""><code>5f419e2</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes a bug where <code>experimental_getFontFileURL()</code> rejected valid font URLs when using the Cloudflare adapter</p>
</li>
<li>
<p><a href="">#17416</a> <a href=""><code>493796b</code></a> Thanks <a href="https://github.com/iseraph-dev"><code>@​iseraph-dev</code></a>! - Skips no-op pathname writes when normalizing SSR request URLs</p>
</li>
<li>
<p><a href="">#17712</a> <a href=""><code>bd374b7</code></a> Thanks <a href="https://github.com/fkatsuhiro"><code>@​fkatsuhiro</code></a>! - Updates deprecation messages target from Astro 7 to 8</p>
</li>
<li>
<p><a href="">#17719</a> <a href=""><code>dac1768</code></a> Thanks <a href="https://github.com/astrobot-houston"><code>@​astrobot-houston</code></a>! - Fixes session ID validation to reject non-UUID cookie values before using them as storage keys</p>
</li>
<li>
<p><a href="">#17770</a> <a href=""><code>84eb7e7</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes <code>--mode</code>, <code>--site</code>, <code>--base</code>, <code>--out-dir</code>, <code>--verbose</code>, <code>--silent</code>, and <code>--open</code> flags being silently dropped when using <code>astro dev --background</code> or <code>astro preview --background</code></p>
</li>
<li>
<p><a href="">#17713</a> <a href=""><code>d035290</code></a> Thanks <a href="https://github.com/wakqasahmed"><code>@​wakqasahmed</code></a>! - Fixes <code>content-modules.mjs</code> not removing entries for deleted or renamed content files, which could cause Vite to attempt to resolve non-existent modules</p>
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
<h2>7.2.9</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17846</a> <a href=""><code>b441180</code></a> Thanks <a href="https://github.com/Princesseuh"><code>@​Princesseuh</code></a>! - Fixes importing <code>.html</code> files not being typed outside of <code>.astro</code> files</p>
</li>
<li>
<p><a href="">#17831</a> <a href=""><code>32e8b44</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes a crash when requesting <code>/index.html</code> against a dynamic page route like <code>[slug].astro</code></p>
</li>
<li>
<p><a href="">#17841</a> <a href=""><code>c35448e</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes SSR manifest containing stale <code>entryModules</code> references to prerender-only chunks that no longer exist in the final build output</p>
</li>
<li>
<p><a href="">#17847</a> <a href=""><code>eb87a23</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes <code>set:text</code> escaping in MDX script and style elements</p>
</li>
</ul>
<h2>7.2.8</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17837</a> <a href=""><code>ecb4082</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Updates the minimum supported version of Sharp to 0.35.4</p>
</li>
<li>
<p><a href="">#17786</a> <a href=""><code>db7c53b</code></a> Thanks <a href="https://github.com/gameroman"><code>@​gameroman</code></a>! - Replaces the internal <code>find-process</code> dependency with a smaller, lighter alternative</p>
</li>
</ul>
<h2>7.2.7</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17415</a> <a href=""><code>55d38c8</code></a> Thanks <a href="https://github.com/iseraph-dev"><code>@​iseraph-dev</code></a>! - Deserializes each route once when loading the SSR manifest</p>
</li>
<li>
<p><a href="">#17772</a> <a href=""><code>023b48b</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes route selection for normalized request paths in adapter and development request handling</p>
</li>
<li>
<p><a href="">#17819</a> <a href=""><code>633855b</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Updates generated and default Cloudflare <code>compatibility_date</code> values to match the installed runtime and requires Wrangler <code>^4.125.0</code></p>
</li>
<li>
<p><a href="">#17813</a> <a href=""><code>ae26d18</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes <code>rewrite()</code> and <code>next(payload)</code> for GET and HEAD requests with host-provided bodies</p>
</li>
<li>
<p><a href="">#17816</a> <a href=""><code>a0d2fe3</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes the experimental <code>svgOptimizer</code> not generating unique per-file ID prefixes when using SVGO's <code>prefixIds</code> plugin</p>
</li>
</ul>
<h2>7.2.6</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#17812</a> <a href=""><code>29af6da</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes a bug where <code>new FetchState(request)</code> could fail in development when server dependencies were optimized</li>
</ul>
<h2>7.2.5</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17758</a> <a href=""><code>5f419e2</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes a bug where <code>experimental_getFontFileURL()</code> rejected valid font URLs when using the Cloudflare adapter</p>
</li>
<li>
<p><a href="">#17416</a> <a href=""><code>493796b</code></a> Thanks <a href="https://github.com/iseraph-dev"><code>@​iseraph-dev</code></a>! - Skips no-op pathname writes when normalizing SSR request URLs</p>
</li>
<li>
<p><a href="">#17712</a> <a href=""><code>bd374b7</code></a> Thanks <a href="https://github.com/fkatsuhiro"><code>@​fkatsuhiro</code></a>! - Updates deprecation messages target from Astro 7 to 8</p>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ad7a332</code></a> [ci] release (<a href="">#17845</a>)</li>
<li><a href=""><code>eb87a23</code></a> Escape set:text values in Astro JSX (<a href="">#17847</a>)</li>
<li><a href=""><code>b441180</code></a> fix(astro): type .html imports outside of .astro files (<a href="">#17846</a>)</li>
<li><a href=""><code>32e8b44</code></a> Guard against stripping /index.html when stripped pathname no longer matches ...</li>
<li><a href=""><code>c35448e</code></a> fix(build): strip prerender-only entry specifiers from SSR manifest (<a href="">#17841</a>)</li>
<li><a href=""><code>7cadf10</code></a> [ci] release (<a href="">#17826</a>)</li>
<li><a href=""><code>ecb4082</code></a> Update Sharp to 0.35.4 (<a href="">#17837</a>)</li>
<li><a href=""><code>8bf6f1a</code></a> chore: split v5/v6 changelogs (<a href="">#17825</a>)</li>
<li><a href=""><code>db7c53b</code></a> chore(deps): replace &quot;find-process&quot; with a smaller, lighter alternative (<a href="">#17786</a>)</li>
<li><a href=""><code>eface15</code></a> [ci] release (<a href="">#17815</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/withastro/astro/commits/astro@7.2.9/packages/astro">compare view</a></li>
</ul>
</details>
<br />

Updates `sharp` from 0.35.3 to 0.35.4
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/lovell/sharp/releases">sharp's releases</a>.</em></p>
<blockquote>
<h2>v0.35.4</h2>
<p><a href="https://github.com/lovell/sharp-libvips/releases/tag/v1.3.3">https://github.com/lovell/sharp-libvips/releases/tag/v1.3.3</a></p>
<ul>
<li>
<p>Bound resize dimensions to coordinate limit.</p>
</li>
<li>
<p>Bound composite left and top to coordinate limit.
<a href="">#4564</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Round palette bit depth up for png and gif colours.
<a href="">#4569</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Ensure tiff.subifd input option is used.
<a href="">#4572</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Ensure <code>info.pages</code> is correct when limiting input page range.
<a href="">#4578</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Improve support for input Streams finishing before output is requested.
<a href="">#4584</a>
<a href="https://github.com/Jaybhade"><code>@​Jaybhade</code></a></p>
</li>
</ul>
<h2>v0.35.4-rc.0</h2>
<ul>
<li>
<p>Upgrade to libvips v8.18.6 for upstream bug fixes.</p>
</li>
<li>
<p>Bound resize dimensions to coordinate limit.</p>
</li>
<li>
<p>Bound composite left and top to coordinate limit.
<a href="">#4564</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Round palette bit depth up for png and gif colours.
<a href="">#4569</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Ensure tiff.subifd input option is used.
<a href="">#4572</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Ensure <code>info.pages</code> is correct when limiting input page range.
<a href="">#4578</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Improve support for input Streams finishing before output is requested.
<a href="">#4584</a>
<a href="https://github.com/Jaybhade"><code>@​Jaybhade</code></a></p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7f1a0a2</code></a> Release v0.35.4</li>
<li><a href=""><code>f927818</code></a> Upgrade to sharp-libvips v1.3.3</li>
<li><a href=""><code>e802092</code></a> Prerelease v0.35.4-rc.0</li>
<li><a href=""><code>e13eb2f</code></a> CI: Fix wasm32 build (<a href="">#4589</a>)</li>
<li><a href=""><code>a82a0b3</code></a> Upgrade to libvips v8.18.6</li>
<li><a href=""><code>8044fe4</code></a> Bound resize dimensions to coordinate limit</li>
<li><a href=""><code>147f859</code></a> Docs: changelog entries for <a href="">#4578</a> <a href="">#4584</a></li>
<li><a href=""><code>ee5bfb8</code></a> Tests: use yauzl directly rather than via extract-zip wrapper</li>
<li><a href=""><code>7a77889</code></a> Bump uraimo/run-on-arch-action from 3.1.0 to 3.2.0 (<a href="">#4588</a>)</li>
<li><a href=""><code>ea5bef2</code></a> Improve support for input Streams finishing before output is requested (<a href="">#4584</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/lovell/sharp/compare/v0.35.3...v0.35.4">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c81b42e94bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.