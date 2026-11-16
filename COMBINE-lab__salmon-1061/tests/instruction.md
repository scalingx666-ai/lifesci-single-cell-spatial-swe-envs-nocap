# Issue

**Title:** build(deps): bump sharp, @astrojs/starlight and astro in /website

## Description

Bumps [sharp](https://github.com/lovell/sharp), [@astrojs/starlight](https://github.com/withastro/starlight/tree/HEAD/packages/starlight) and [astro](https://github.com/withastro/astro/tree/HEAD/packages/astro). These dependencies needed to be updated together.
Updates `sharp` from 0.34.5 to 0.35.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/lovell/sharp/releases">sharp's releases</a>.</em></p>
<blockquote>
<h2>v0.35.3</h2>
<ul>
<li>
<p>Tighten verification of <code>text</code> dimensions, TIFF tile dimensions and <code>extend</code> values.</p>
</li>
<li>
<p>Improve code bundler support by resolving path to libvips binary.</p>
</li>
<li>
<p>Increase default concurrency when use of <code>MALLOC_ARENA_MAX</code> is detected.</p>
</li>
<li>
<p>Emit warning about binaries provided by Electron for use on Linux.</p>
</li>
<li>
<p>Add <code>hasAlpha</code> property to output <code>info</code>.
<a href="">#4500</a></p>
</li>
<li>
<p>TypeScript: Return more precise <code>Buffer&lt;ArrayBuffer&gt;</code> from <code>toBuffer</code>.
<a href="">#4520</a>
<a href="https://github.com/Andarist"><code>@​Andarist</code></a></p>
</li>
<li>
<p>Bound <code>clahe</code> width and height to avoid signed overflow.
<a href="">#4551</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Bound <code>trim</code> margin to avoid signed overflow.
<a href="">#4552</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Reject infinite values when validating numbers.
<a href="">#4553</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Bound extract region to libvips coordinate limit.
<a href="">#4555</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Verify background colour values are numbers.
<a href="">#4556</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Bound create and raw input dimensions to coordinate limit.
<a href="">#4558</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Tighten recomb and affine matrix verification.
<a href="">#4560</a>
<a href="https://github.com/chatman-media"><code>@​chatman-media</code></a></p>
</li>
<li>
<p>Verify cache memory limit to avoid overflow.
<a href="">#4561</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
</ul>
<h2>v0.35.3-rc.2</h2>
<ul>
<li>Tighten verification of <code>text</code> dimensions, TIFF tile dimensions and <code>extend</code> values.</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1018449</code></a> Release v0.35.3</li>
<li><a href=""><code>ba303a7</code></a> Prerelease v0.35.3-rc.2</li>
<li><a href=""><code>4f94fc5</code></a> Upgrade to sharp-libvips v1.3.2</li>
<li><a href=""><code>c5e7a3f</code></a> Bump devDeps, fix Deno/Windows smoke tests</li>
<li><a href=""><code>9a8d002</code></a> Docs: Add changelog entry and note about transferable <a href="">#4520</a></li>
<li><a href=""><code>8694db0</code></a> TypeScript: Return more precise <code>Buffer\&lt;ArrayBuffer&gt;</code> from <code>toBuffer</code> (<a href="">#4520</a>)</li>
<li><a href=""><code>e000d0b</code></a> Prerelease v0.35.3-rc.1</li>
<li><a href=""><code>9554ca9</code></a> Prerelease v0.35.3-rc.0</li>
<li><a href=""><code>6a29fd5</code></a> Emit warning about native binaries on Linux Electron</li>
<li><a href=""><code>540d2ea</code></a> Increase default concurrency when use of MALLOC_ARENA_MAX detected</li>
<li>Additional commits viewable in <a href="https://github.com/lovell/sharp/compare/v0.34.5...v0.35.3">compare view</a></li>
</ul>
</details>
<br />

Updates `@astrojs/starlight` from 0.38.5 to 0.41.4
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/withastro/starlight/releases">@​astrojs/starlight's releases</a>.</em></p>
<blockquote>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.41.4</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#3936</a> <a href=""><code>712eedd</code></a> Thanks <a href="https://github.com/miichom"><code>@​miichom</code></a>! - Fixes support for modifying Zod enums when passing an <a href="https://starlight.astro.build/reference/frontmatter/#extend"><code>extend</code> option</a> to Starlight’s <code>docsSchema()</code></p>
</li>
<li>
<p><a href="">#4092</a> <a href=""><code>0896b91</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Fixes support for links containing a protocol like <code>mailto:</code> in the sidebar</p>
</li>
<li>
<p><a href="">#4088</a> <a href=""><code>4486ba4</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Simplifies Starlight’s client-side sidebar state persistence script slightly</p>
</li>
</ul>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.41.3</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#3911</a> <a href=""><code>1686ecc</code></a> Thanks <a href="https://github.com/timothyjordan"><code>@​timothyjordan</code></a>! - Keeps keyboard focus inside the mobile menu while it is open, preventing focus moving to hidden interactive elements in page content.</li>
</ul>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.41.2</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#4008</a> <a href=""><code>58a3520</code></a> Thanks <a href="https://github.com/FrancoKaddour"><code>@​FrancoKaddour</code></a>! - Fixes the table of contents overflowing the right edge of the viewport when a custom <code>--sl-content-width</code> value exceeds available space</p>
</li>
<li>
<p><a href="">#4015</a> <a href=""><code>bdbfffc</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Fixes an issue where aside icons were rendered incorrectly in projects where Astro’s MDX integration had optimization disabled</p>
</li>
</ul>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.41.1</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#3967</a> <a href=""><code>72e63dc</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Adds 2 new icons: <code>link</code> and <code>link-alt</code>.</p>
</li>
<li>
<p><a href="">#3988</a> <a href=""><code>ac55cfa</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Fixes a dependency resolution issue introduced in Starlight v0.41</p>
</li>
<li>
<p><a href="">#3967</a> <a href=""><code>72e63dc</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Optimizes the icons of Markdown asides.</p>
</li>
</ul>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.41.0</h2>
<h3>Minor Changes</h3>
<ul>
<li>
<p><a href="">#3951</a> <a href=""><code>1202dd4</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Adds support for Astro v7, drops support for Astro v6.</p>
<h4>Upgrade Astro and dependencies</h4>
<p>⚠️ <strong>BREAKING CHANGE:</strong> Astro v6 is no longer supported. Make sure you <a href="https://docs.astro.build/en/guides/upgrade-to/v7/">update Astro</a> and any other official integrations at the same time as updating Starlight:</p>
<pre lang="sh"><code>npx @astrojs/upgrade
</code></pre>
<p><em>Community Starlight plugins and Astro integrations may also need to be manually updated to work with Astro v7. If you encounter any issues, please reach out to the plugin or integration author to see if it is a known issue or if an updated version is being worked on.</em></p>
<p>⚠️ <strong>BREAKING CHANGE:</strong> This release drops official support for Chromium-based browsers prior to version 111 (released 07 March 2023) and Safari-based browsers prior to version 16.4 (released 27 March 2023). You can find a list of currently supported browsers and their versions using this <a href="https://browsersl.ist/#q=%3E+0.5%25%2C+not+dead%2C+Chrome+%3E%3D+111%2C+Edge+%3E%3D+111%2C+Firefox+%3E%3D+121%2C+Safari+%3E%3D+16.4%2C+iOS+%3E%3D+16.4%2C+not+op_mini+all">browserslist query</a>.</p>
</li>
</ul>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#3953</a> <a href=""><code>a935d33</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Fixes Starlight Markdown processing being potentially applied to files that should not be processed.</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/withastro/starlight/blob/main/packages/starlight/CHANGELOG.md">@​astrojs/starlight's changelog</a>.</em></p>
<blockquote>
<h2>0.41.4</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#3936</a> <a href=""><code>712eedd</code></a> Thanks <a href="https://github.com/miichom"><code>@​miichom</code></a>! - Fixes support for modifying Zod enums when passing an <a href="https://starlight.astro.build/reference/frontmatter/#extend"><code>extend</code> option</a> to Starlight’s <code>docsSchema()</code></p>
</li>
<li>
<p><a href="">#4092</a> <a href=""><code>0896b91</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Fixes support for links containing a protocol like <code>mailto:</code> in the sidebar</p>
</li>
<li>
<p><a href="">#4088</a> <a href=""><code>4486ba4</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Simplifies Starlight’s client-side sidebar state persistence script slightly</p>
</li>
</ul>
<h2>0.41.3</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#3911</a> <a href=""><code>1686ecc</code></a> Thanks <a href="https://github.com/timothyjordan"><code>@​timothyjordan</code></a>! - Keeps keyboard focus inside the mobile menu while it is open, preventing focus moving to hidden interactive elements in page content.</li>
</ul>
<h2>0.41.2</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#4008</a> <a href=""><code>58a3520</code></a> Thanks <a href="https://github.com/FrancoKaddour"><code>@​FrancoKaddour</code></a>! - Fixes the table of contents overflowing the right edge of the viewport when a custom <code>--sl-content-width</code> value exceeds available space</p>
</li>
<li>
<p><a href="">#4015</a> <a href=""><code>bdbfffc</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Fixes an issue where aside icons were rendered incorrectly in projects where Astro’s MDX integration had optimization disabled</p>
</li>
</ul>
<h2>0.41.1</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#3967</a> <a href=""><code>72e63dc</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Adds 2 new icons: <code>link</code> and <code>link-alt</code>.</p>
</li>
<li>
<p><a href="">#3988</a> <a href=""><code>ac55cfa</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Fixes a dependency resolution issue introduced in Starlight v0.41</p>
</li>
<li>
<p><a href="">#3967</a> <a href=""><code>72e63dc</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Optimizes the icons of Markdown asides.</p>
</li>
</ul>
<h2>0.41.0</h2>
<h3>Minor Changes</h3>
<ul>
<li>
<p><a href="">#3951</a> <a href=""><code>1202dd4</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Adds support for Astro v7, drops support for Astro v6.</p>
<h4>Upgrade Astro and dependencies</h4>
<p>⚠️ <strong>BREAKING CHANGE:</strong> Astro v6 is no longer supported. Make sure you <a href="https://docs.astro.build/en/guides/upgrade-to/v7/">update Astro</a> and any other official integrations at the same time as updating Starlight:</p>
<pre lang="sh"><code>npx @astrojs/upgrade
</code></pre>
<p><em>Community Starlight plugins and Astro integrations may also need to be manually updated to work with Astro v7. If you encounter any issues, please reach out to the plugin or integration author to see if it is a known issue or if an updated version is being worked on.</em></p>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ab2792b</code></a> [ci] release (<a href="">#4090</a>)</li>
<li><a href=""><code>712eedd</code></a> fix: invalid option error when modifying enums in docsSchema's extend (<a href="">#3936</a>)</li>
<li><a href=""><code>0896b91</code></a> Support links with any protocol in sidebars (<a href="">#4092</a>)</li>
<li><a href=""><code>4486ba4</code></a> Remove pagehide event from sidebar persistence script (<a href="">#4088</a>)</li>
<li><a href=""><code>96cee6e</code></a> [ci] release (<a href="">#4032</a>)</li>
<li><a href=""><code>1686ecc</code></a> fix(MobileMenuToggle): trap keyboard focus inside the mobile menu (<a href="">#3911</a>)</li>
<li><a href=""><code>3948048</code></a> [ci] release (<a href="">#4016</a>)</li>
<li><a href=""><code>1a209c5</code></a> [ci] format</li>
<li><a href=""><code>58a3520</code></a> fix(css): prevent TOC overflow with custom --sl-content-width (<a href="">#4008</a>)</li>
<li><a href=""><code>bdbfffc</code></a> Fix aside icons when MDX optimization is disabled (<a href="">#4015</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/withastro/starlight/commits/@astrojs/starlight@0.41.4/packages/starlight">compare view</a></li>
</ul>
</details>
<br />

Updates `astro` from 6.4.6 to 7.1.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/withastro/astro/releases">astro's releases</a>.</em></p>
<blockquote>
<h2>astro@7.1.3</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#17427</a> <a href=""><code>630b382</code></a> Thanks <a href="https://github.com/astrobot-houston"><code>@​astrobot-houston</code></a>! - Fixes image optimization during <code>astro build</code> using too many parallel processes in CPU-limited containers. Builds now respect the container's CPU limit, reducing peak memory usage and avoiding out-of-memory crashes.
<!-- raw HTML omitted -->
<!-- raw HTML omitted --></li>
</ul>
<h2>astro@7.1.2</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17445</a> <a href=""><code>a5f7230</code></a> Thanks <a href="https://github.com/ocavue"><code>@​ocavue</code></a>! - Updates dependency <code>cookie</code> to v2. Cookie values made entirely of URL-safe characters are no longer percent-encoded in <code>Set-Cookie</code> headers; encoded values round-trip exactly as before.</p>
</li>
<li>
<p><a href="">#17402</a> <a href=""><code>a89c137</code></a> Thanks <a href="https://github.com/farrosfr"><code>@​farrosfr</code></a>! - Fixes a bug where mutated <code>Astro.locals</code> during the request lifecycle are lost and not passed to custom error pages (<code>404.astro</code>/<code>500.astro</code>)</p>
</li>
<li>
<p><a href="">#17405</a> <a href=""><code>91992ef</code></a> Thanks <a href="https://github.com/Araluma"><code>@​Araluma</code></a>! - Prevents an unhandled promise rejection from the prefetch <code>fetch</code> fallback. In WebKit (Safari), <code>&lt;link rel=&quot;prefetch&quot;&gt;</code> is unsupported, so prefetch uses the <code>fetch()</code> fallback; on a flaky connection that fetch rejects with <code>TypeError: Load failed</code>, and because the promise was not awaited or caught, it surfaced as an unhandled rejection to the page's global error handlers. The best-effort prefetch now swallows the failure with <code>.catch()</code>.</p>
</li>
</ul>
<h2>astro@7.1.1</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#17399</a> <a href=""><code>4b03702</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes encoded request paths being routed incorrectly when using domain-based i18n</li>
</ul>
<h2>astro@7.1.0</h2>
<h3>Minor Changes</h3>
<ul>
<li>
<p><a href="">#17302</a> <a href=""><code>5f4dc03</code></a> Thanks <a href="https://github.com/astrobot-houston"><code>@​astrobot-houston</code></a>! - Adds a new <code>deferRender</code> option to the <code>glob()</code> content loader</p>
<p>When set to <code>true</code>, renderable entries (such as Markdown) are not rendered during content sync. Instead, rendering is deferred until the entry is actually rendered in a page, using the same on-demand path that <code>.mdx</code> files already use.</p>
<p>This reduces memory usage during <code>astro build</code> for large collections whose rendered output is much larger than the source — for example, Markdown that uses heavy rehype plugins like <code>rehype-katex</code>. Such builds could previously run out of memory while storing the eagerly-rendered HTML for every entry.</p>
<pre lang="js"><code>// src/content.config.ts
import { defineCollection } from 'astro:content';
import { glob } from 'astro/loaders';
<p>const docs = defineCollection({
loader: glob({ pattern: '**/*.md', base: 'src/content/docs', deferRender: true }),
});
</code></pre></p>
<p>By default <code>deferRender</code> is <code>false</code>, preserving the existing behavior of rendering entries eagerly during sync so their rendered HTML can be cached across builds.</p>
</li>
<li>
<p><a href="">#17296</a> <a href=""><code>30698a2</code></a> Thanks <a href="https://github.com/ematipico"><code>@​ematipico</code></a>! - Adds a new experimental <code>collectionStorage</code> option for controlling how the content layer persists its data store</p>
<p>By default, Astro serializes the entire content layer data store to a single file (<code>.astro/data-store.json</code>). For very large content collections, this file can grow large enough to hit platform file-size limits.</p>
<p>Set <code>experimental.collectionStorage: 'chunked'</code> to instead split the data store across many smaller, content-addressed files inside a <code>.astro/data-store/</code> directory, described by a manifest:</p>
<pre lang="js"><code>// astro.config.mjs
</code></pre>
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
<h2>7.1.3</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#17427</a> <a href=""><code>630b382</code></a> Thanks <a href="https://github.com/astrobot-houston"><code>@​astrobot-houston</code></a>! - Fixes image optimization during <code>astro build</code> using too many parallel processes in CPU-limited containers. Builds now respect the container's CPU limit, reducing peak memory usage and avoiding out-of-memory crashes.
<!-- raw HTML omitted -->
<!-- raw HTML omitted --></li>
</ul>
<h2>7.1.2</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17445</a> <a href=""><code>a5f7230</code></a> Thanks <a href="https://github.com/ocavue"><code>@​ocavue</code></a>! - Updates dependency <code>cookie</code> to v2. Cookie values made entirely of URL-safe characters are no longer percent-encoded in <code>Set-Cookie</code> headers; encoded values round-trip exactly as before.</p>
</li>
<li>
<p><a href="">#17402</a> <a href=""><code>a89c137</code></a> Thanks <a href="https://github.com/farrosfr"><code>@​farrosfr</code></a>! - Fixes a bug where mutated <code>Astro.locals</code> during the request lifecycle are lost and not passed to custom error pages (<code>404.astro</code>/<code>500.astro</code>)</p>
</li>
<li>
<p><a href="">#17405</a> <a href=""><code>91992ef</code></a> Thanks <a href="https://github.com/Araluma"><code>@​Araluma</code></a>! - Prevents an unhandled promise rejection from the prefetch <code>fetch</code> fallback. In WebKit (Safari), <code>&lt;link rel=&quot;prefetch&quot;&gt;</code> is unsupported, so prefetch uses the <code>fetch()</code> fallback; on a flaky connection that fetch rejects with <code>TypeError: Load failed</code>, and because the promise was not awaited or caught, it surfaced as an unhandled rejection to the page's global error handlers. The best-effort prefetch now swallows the failure with <code>.catch()</code>.</p>
</li>
</ul>
<h2>7.1.1</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#17399</a> <a href=""><code>4b03702</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes encoded request paths being routed incorrectly when using domain-based i18n</li>
</ul>
<h2>7.1.0</h2>
<h3>Minor Changes</h3>
<ul>
<li>
<p><a href="">#17302</a> <a href=""><code>5f4dc03</code></a> Thanks <a href="https://github.com/astrobot-houston"><code>@​astrobot-houston</code></a>! - Adds a new <code>deferRender</code> option to the <code>glob()</code> content loader</p>
<p>When set to <code>true</code>, renderable entries (such as Markdown) are not rendered during content sync. Instead, rendering is deferred until the entry is actually rendered in a page, using the same on-demand path that <code>.mdx</code> files already use.</p>
<p>This reduces memory usage during <code>astro build</code> for large collections whose rendered output is much larger than the source — for example, Markdown that uses heavy rehype plugins like <code>rehype-katex</code>. Such builds could previously run out of memory while storing the eagerly-rendered HTML for every entry.</p>
<pre lang="js"><code>// src/content.config.ts
import { defineCollection } from 'astro:content';
import { glob } from 'astro/loaders';
<p>const docs = defineCollection({
loader: glob({ pattern: '**/*.md', base: 'src/content/docs', deferRender: true }),
});
</code></pre></p>
<p>By default <code>deferRender</code> is <code>false</code>, preserving the existing behavior of rendering entries eagerly during sync so their rendered HTML can be cached across builds.</p>
</li>
<li>
<p><a href="">#17296</a> <a href=""><code>30698a2</code></a> Thanks <a href="https://github.com/ematipico"><code>@​ematipico</code></a>! - Adds a new experimental <code>collectionStorage</code> option for controlling how the content layer persists its data store</p>
<p>By default, Astro serializes the entire content layer data store to a single file (<code>.astro/data-store.json</code>). For very large content collections, this file can grow large enough to hit platform file-size limits.</p>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cf9ffc7</code></a> [ci] release (<a href="">#17455</a>)</li>
<li><a href=""><code>630b382</code></a> Use <code>os.availableParallelism()</code> for image optimization queue to fix OOM in CP...</li>
<li><a href=""><code>8a7f7e0</code></a> [ci] release (<a href="">#17411</a>)</li>
<li><a href=""><code>ebbd793</code></a> chore(deps): update <code>astro-embed</code> (<a href="">#17436</a>)</li>
<li><a href=""><code>311e42c</code></a> [ci] format</li>
<li><a href=""><code>1d62202</code></a> chore(deps): update <code>neotraverse</code> to v1 (<a href="">#17446</a>)</li>
<li><a href=""><code>a5f7230</code></a> fix(astro): update <code>cookie</code> to v2 (<a href="">#17445</a>)</li>
<li><a href=""><code>91992ef</code></a> fix(prefetch): swallow fetch-fallback rejection to avoid unhandled 'Load fail...</li>
<li><a href=""><code>a89c137</code></a> fix(astro): propagate mutated locals to custom error pages (<a href="">#17402</a>)</li>
<li><a href=""><code>91c645a</code></a> [ci] release (<a href="">#17403</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/withastro/astro/commits/astro@7.1.3/packages/astro">compare view</a></li>
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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/COMBINE-lab/salmon/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea416223b54b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.