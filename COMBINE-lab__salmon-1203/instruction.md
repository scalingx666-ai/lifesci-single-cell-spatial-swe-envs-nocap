# Issue

**Title:** chore(deps): bump the website-minor group across 1 directory with 2 updates

## Description

Bumps the website-minor group with 2 updates in the /website directory: [@astrojs/starlight](https://github.com/withastro/starlight/tree/HEAD/packages/starlight) and [astro](https://github.com/withastro/astro/tree/HEAD/packages/astro).

Updates `@astrojs/starlight` from 0.41.9 to 0.42.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/withastro/starlight/releases">@​astrojs/starlight's releases</a>.</em></p>
<blockquote>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.42.2</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4201</a> <a href=""><code>fafd989</code></a> Thanks <a href="https://github.com/linux-universe"><code>@​linux-universe</code></a>! - Add 1 new icon: <code>fluxer</code></li>
</ul>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.42.1</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4198</a> <a href=""><code>96a44d4</code></a> Thanks <a href="https://github.com/mayank99"><code>@​mayank99</code></a>! - Removes the <code>popover</code> attribute from the sidebar pane on desktop viewports. This ensures the desktop sidebar doesn't stay in a &quot;hidden&quot; popover visibility state.</li>
</ul>
<h2><code>@​astrojs/starlight</code><a href="https://github.com/0"><code>@​0</code></a>.42.0</h2>
<h3>Minor Changes</h3>
<ul>
<li>
<p><a href="">#3572</a> <a href=""><code>292fb17</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Distributes package as JavaScript files with dedicated type declaration files instead of TypeScript source files.</p>
</li>
<li>
<p><a href="">#4121</a> <a href=""><code>2623ae6</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Simplifies markup for Starlight’s mobile menu toggle</p>
<p><strong>⚠️ Potentially breaking change:</strong> If you use a theme plugin, custom styles, or component overrides targeting the <code>MobileMenuToggle</code> button or <code>PageFrame</code> components, you may need to adjust these for the new markup. The button is no longer wrapped in a <code>&lt;starlight-menu-button&gt;</code> custom element and no longer uses the <code>aria-expanded</code> attribute. Instead, you can use the <code>.sl-menu-button</code> class name to target the button and the <code>:popover-open</code> pseudo-class to style the menu open state specifically.</p>
<p>In the following example, custom styles for the menu button are updated for the new approach:</p>
<pre lang="diff"><code>- starlight-menu-button button {
+ .sl-menu-button {
  color: var(--sl-color-text);
}
<ul>
<li>starlight-menu-button[aria-expanded='true'] button {</li>
</ul>
<ul>
<li>.sl-menu-button:has(~ :popover-open) {
color: var(--sl-color-text-accent-high);
}
</code></pre></li>
</ul>
<p>See <a href="https://github.com/withastro/starlight/blob/main/packages/starlight/components/MobileMenuToggle.astro"><code>MobileMenuToggle.astro</code></a> and <a href="https://github.com/withastro/starlight/blob/main/packages/starlight/components/PageFrame.astro"><code>PageFrame.astro</code></a> on GitHub for the full source code of the updated components.</p>
</li>
<li>
<p><a href="">#3572</a> <a href=""><code>292fb17</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Removes the <code>tagline</code> configuration option, which was never used.</p>
<p>If your configuration included a <code>tagline</code> option, you can safely remove it without any replacement.</p>
</li>
<li>
<p><a href="">#4134</a> <a href=""><code>6135f01</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Updates internal <code>@astrojs/mdx</code>, <code>@astrojs/markdown-satteri</code>, and <code>satteri</code> dependencies.</p>
<p>⚠️ <strong>BREAKING CHANGE:</strong> The following minimum versions are now required:</p>
<ul>
<li><code>astro</code> v7.2.10 or later</li>
<li><code>@astrojs/markdown-satteri</code> 0.4.0 or later (if you use it)</li>
<li><code>@astrojs/markdown-remark</code> 7.3.0 or later (if you use it)</li>
</ul>
<p>Please update Starlight and Astro together:</p>
<pre lang="sh"><code></code></pre>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/withastro/starlight/blob/main/packages/starlight/CHANGELOG.md">@​astrojs/starlight's changelog</a>.</em></p>
<blockquote>
<h2>0.42.2</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4201</a> <a href=""><code>fafd989</code></a> Thanks <a href="https://github.com/linux-universe"><code>@​linux-universe</code></a>! - Add 1 new icon: <code>fluxer</code></li>
</ul>
<h2>0.42.1</h2>
<h3>Patch Changes</h3>
<ul>
<li><a href="">#4198</a> <a href=""><code>96a44d4</code></a> Thanks <a href="https://github.com/mayank99"><code>@​mayank99</code></a>! - Removes the <code>popover</code> attribute from the sidebar pane on desktop viewports. This ensures the desktop sidebar doesn't stay in a &quot;hidden&quot; popover visibility state.</li>
</ul>
<h2>0.42.0</h2>
<h3>Minor Changes</h3>
<ul>
<li>
<p><a href="">#3572</a> <a href=""><code>292fb17</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Distributes package as JavaScript files with dedicated type declaration files instead of TypeScript source files.</p>
</li>
<li>
<p><a href="">#4121</a> <a href=""><code>2623ae6</code></a> Thanks <a href="https://github.com/delucis"><code>@​delucis</code></a>! - Simplifies markup for Starlight’s mobile menu toggle</p>
<p><strong>⚠️ Potentially breaking change:</strong> If you use a theme plugin, custom styles, or component overrides targeting the <code>MobileMenuToggle</code> button or <code>PageFrame</code> components, you may need to adjust these for the new markup. The button is no longer wrapped in a <code>&lt;starlight-menu-button&gt;</code> custom element and no longer uses the <code>aria-expanded</code> attribute. Instead, you can use the <code>.sl-menu-button</code> class name to target the button and the <code>:popover-open</code> pseudo-class to style the menu open state specifically.</p>
<p>In the following example, custom styles for the menu button are updated for the new approach:</p>
<pre lang="diff"><code>- starlight-menu-button button {
+ .sl-menu-button {
  color: var(--sl-color-text);
}
<ul>
<li>starlight-menu-button[aria-expanded='true'] button {</li>
</ul>
<ul>
<li>.sl-menu-button:has(~ :popover-open) {
color: var(--sl-color-text-accent-high);
}
</code></pre></li>
</ul>
<p>See <a href="https://github.com/withastro/starlight/blob/main/packages/starlight/components/MobileMenuToggle.astro"><code>MobileMenuToggle.astro</code></a> and <a href="https://github.com/withastro/starlight/blob/main/packages/starlight/components/PageFrame.astro"><code>PageFrame.astro</code></a> on GitHub for the full source code of the updated components.</p>
</li>
<li>
<p><a href="">#3572</a> <a href=""><code>292fb17</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Removes the <code>tagline</code> configuration option, which was never used.</p>
<p>If your configuration included a <code>tagline</code> option, you can safely remove it without any replacement.</p>
</li>
<li>
<p><a href="">#4134</a> <a href=""><code>6135f01</code></a> Thanks <a href="https://github.com/HiDeoo"><code>@​HiDeoo</code></a>! - Updates internal <code>@astrojs/mdx</code>, <code>@astrojs/markdown-satteri</code>, and <code>satteri</code> dependencies.</p>
<p>⚠️ <strong>BREAKING CHANGE:</strong> The following minimum versions are now required:</p>
<ul>
<li><code>astro</code> v7.2.10 or later</li>
<li><code>@astrojs/markdown-satteri</code> 0.4.0 or later (if you use it)</li>
<li><code>@astrojs/markdown-remark</code> 7.3.0 or later (if you use it)</li>
</ul>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>525590a</code></a> [ci] release (<a href="">#4206</a>)</li>
<li><a href=""><code>fafd989</code></a> add Fluxer icon (<a href="">#4201</a>)</li>
<li><a href=""><code>a852070</code></a> [ci] release (<a href="">#4199</a>)</li>
<li><a href=""><code>96a44d4</code></a> remove <code>popover</code> attribute from sidebar-pane on wide viewports (<a href="">#4198</a>)</li>
<li><a href=""><code>88ad3c2</code></a> [ci] release (<a href="">#4172</a>)</li>
<li><a href=""><code>74cb3f1</code></a> Update dependencies (<a href="">#4173</a>)</li>
<li><a href=""><code>6135f01</code></a> Use Sätteri 0.10 APIs (<a href="">#4134</a>)</li>
<li><a href=""><code>2623ae6</code></a> Refactor mobile menu to use Popover API (<a href="">#4121</a>)</li>
<li><a href=""><code>09af1c6</code></a> chore(deps): update <code>magic-string</code> to v1 (<a href="">#4082</a>)</li>
<li><a href=""><code>292fb17</code></a> [i18nIgnore] Transpile Starlight packages (<a href="">#3572</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/withastro/starlight/commits/@astrojs/starlight@0.42.2/packages/starlight">compare view</a></li>
</ul>
</details>
<br />

Updates `astro` from 7.2.9 to 7.3.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/withastro/astro/releases">astro's releases</a>.</em></p>
<blockquote>
<h2>astro@7.3.3</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17651</a> <a href=""><code>504333c</code></a> Thanks <a href="https://github.com/sxzz"><code>@​sxzz</code></a>! - Refactors internal version handling to use a smaller, ESM-native dependency</p>
</li>
<li>
<p><a href="">#17942</a> <a href=""><code>0bc5715</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Returns appropriate 400 and 404 responses from the image endpoint for invalid and missing local image paths</p>
</li>
<li>
<p><a href="">#17700</a> <a href=""><code>b2222fc</code></a> Thanks <a href="https://github.com/winklemad"><code>@​winklemad</code></a>! - Fixes <code>Astro.preferredLocaleList</code> returning an empty list when a locale is configured with the object form (<code>{ path, codes }</code>) and the browser sends the code with different casing or an underscore, such as <code>en-US</code> matching a configured <code>en-us</code></p>
</li>
<li>
<p><a href="">#17941</a> <a href=""><code>394ff79</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes <code>astro preview --ignore-lock</code> (and <code>astro dev --ignore-lock</code>) being refused when run from an AI agent environment. The flag now starts the server in the foreground instead of erroring, since agent detection only inferred background mode and was never explicitly requested. An explicit <code>--background</code> combined with <code>--ignore-lock</code> still errors.</p>
</li>
<li>
<p><a href="">#17928</a> <a href=""><code>3277927</code></a> Thanks <a href="https://github.com/ArmandPhilippot"><code>@​ArmandPhilippot</code></a>! - Fixes TypeScript autocompletion for <code>getImage()</code> to suggest all available predefined options.</p>
</li>
<li>
<p><a href="">#17928</a> <a href=""><code>3277927</code></a> Thanks <a href="https://github.com/ArmandPhilippot"><code>@​ArmandPhilippot</code></a>! - Fixes a type error in <code>getImage()</code> options that allowed passing both <code>widths</code> and <code>densities</code> at the same time.</p>
</li>
<li>
<p><a href="">#17857</a> <a href=""><code>2637ed1</code></a> Thanks <a href="https://github.com/Princesseuh"><code>@​Princesseuh</code></a>! - Improves rendering performance</p>
</li>
<li>
<p><a href="">#17943</a> <a href=""><code>2fc7ce9</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes a WebAssembly error when importing <code>astro:actions</code> in tests that run under <code>@cloudflare/vitest-pool-workers</code></p>
</li>
<li>
<p><a href="">#18018</a> <a href=""><code>1b5a234</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes trailing-slash redirect response body pointing to the incoming URL instead of the redirect target. The <code>location</code> header was correct, but the HTML body (<code>&lt;meta http-equiv=&quot;refresh&quot;&gt;</code>, <code>&lt;title&gt;</code>, and <code>&lt;a&gt;</code> tag) contained the original request path without the trailing-slash correction or query string.</p>
</li>
<li>
<p><a href="">#17905</a> <a href=""><code>eaf70fa</code></a> Thanks <a href="https://github.com/SudoDevStudio"><code>@​SudoDevStudio</code></a>! - Fixes custom dev toolbar apps losing their UI after client-side navigation with <code>&lt;ClientRouter /&gt;</code>.</p>
</li>
<li>
<p><a href="">#18011</a> <a href=""><code>558b301</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes prerendered Cloudflare pages rendering as <code>[object Object]</code> when <code>nodejs_compat</code> is enabled in <code>wrangler.toml</code></p>
</li>
<li>
<p><a href="">#17944</a> <a href=""><code>ba08e35</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes a regression in <code>astro dev</code> where writes outside the module graph (for example, <code>@astrojs/cloudflare</code>'s <code>.wrangler/state</code> files) invalidated the middleware on every request, causing repeated SSR reloads. Such writes no longer invalidate the middleware.</p>
</li>
<li>
<p><a href="">#17531</a> <a href=""><code>ae837db</code></a> Thanks <a href="https://github.com/danilloestrela"><code>@​danilloestrela</code></a>! - Updates <code>svgo</code> to <code>4.0.2</code> to resolve a security advisory</p>
</li>
<li>
<p><a href="">#17953</a> <a href=""><code>dbbf10e</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes a one-time page reload shortly after the first load on cold dev-server starts when a project has framework components imported from MDX content entries. MDX files are now included in the dev dependency pre-bundling scan, so their framework dependencies are bundled up front instead of being discovered (and reloaded for) at runtime.</p>
</li>
<li>
<p><a href="">#17955</a> <a href=""><code>4e8ad9a</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Improves dev server startup time. The content config and dev server app module graphs now begin compiling during server creation without blocking the server from listening. Request handling waits for the shared setup result when needed, cutting <code>astro dev</code> ready time by roughly a third on projects with a content config.</p>
</li>
<li>
<p><a href="">#17960</a> <a href=""><code>9838049</code></a> Thanks <a href="https://github.com/Chy-Zaber-Bin-Zahid"><code>@​Chy-Zaber-Bin-Zahid</code></a>! - Improves the diagnostics of some Astro errors.</p>
</li>
<li>
<p><a href="">#17998</a> <a href=""><code>0e5478d</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes SVG <code>&lt;style&gt;</code> elements nested inside <code>&lt;defs&gt;</code> or other container elements not being hashed for CSP</p>
</li>
<li>
<p><a href="">#17994</a> <a href=""><code>80f9f1d</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes <code>experimental.incrementalBuild</code> restoring pages with stale CSS after a preprocessor partial changes or missing original images referenced by restored pages</p>
</li>
<li>
<p><a href="">#17889</a> <a href=""><code>8ae6b46</code></a> Thanks <a href="https://github.com/ajfAfg"><code>@​ajfAfg</code></a>! - Fixes a bug where the dev server stripped the configured <code>base</code> from URLs that only share a prefix with it. With <code>base: '/s'</code>, requests to <code>/src/...</code> were rewritten to <code>/rc/...</code> and failed, breaking those pages during development.</p>
</li>
<li>
<p><a href="">#17980</a> <a href=""><code>cfccafa</code></a> Thanks <a href="https://github.com/gameroman"><code>@​gameroman</code></a>! - Improves JSDoc for fonts api</p>
</li>
<li>
<p><a href="">#17953</a> <a href=""><code>dbbf10e</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes CSS HMR for framework components rendered through content entries after <code>ClientRouter</code> navigation</p>
</li>
<li>
<p><a href="">#17970</a> <a href=""><code>0b4dc3a</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Improves serialization of transition animation values in generated CSS</p>
</li>
<li>
<p><a href="">#17999</a> <a href=""><code>30ef3cb</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes content collection HMR not updating prerendered pages when an adapter enables a separate prerender environment (e.g. <code>@astrojs/cloudflare</code> with <code>prerenderEnvironment: 'node'</code>)</p>
</li>
<li>
<p><a href="">#18002</a> <a href=""><code>312ab49</code></a> Thanks <a href="https://github.com/shoutoutuoadi325"><code>@​shoutoutuoadi325</code></a>! - Fixes redirect targets being corrupted when a dynamic route parameter value contains <code>$</code> replacement patterns like <code>$&amp;</code></p>
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
<h2>7.3.3</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#17651</a> <a href=""><code>504333c</code></a> Thanks <a href="https://github.com/sxzz"><code>@​sxzz</code></a>! - Refactors internal version handling to use a smaller, ESM-native dependency</p>
</li>
<li>
<p><a href="">#17942</a> <a href=""><code>0bc5715</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Returns appropriate 400 and 404 responses from the image endpoint for invalid and missing local image paths</p>
</li>
<li>
<p><a href="">#17700</a> <a href=""><code>b2222fc</code></a> Thanks <a href="https://github.com/winklemad"><code>@​winklemad</code></a>! - Fixes <code>Astro.preferredLocaleList</code> returning an empty list when a locale is configured with the object form (<code>{ path, codes }</code>) and the browser sends the code with different casing or an underscore, such as <code>en-US</code> matching a configured <code>en-us</code></p>
</li>
<li>
<p><a href="">#17941</a> <a href=""><code>394ff79</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes <code>astro preview --ignore-lock</code> (and <code>astro dev --ignore-lock</code>) being refused when run from an AI agent environment. The flag now starts the server in the foreground instead of erroring, since agent detection only inferred background mode and was never explicitly requested. An explicit <code>--background</code> combined with <code>--ignore-lock</code> still errors.</p>
</li>
<li>
<p><a href="">#17928</a> <a href=""><code>3277927</code></a> Thanks <a href="https://github.com/ArmandPhilippot"><code>@​ArmandPhilippot</code></a>! - Fixes TypeScript autocompletion for <code>getImage()</code> to suggest all available predefined options.</p>
</li>
<li>
<p><a href="">#17928</a> <a href=""><code>3277927</code></a> Thanks <a href="https://github.com/ArmandPhilippot"><code>@​ArmandPhilippot</code></a>! - Fixes a type error in <code>getImage()</code> options that allowed passing both <code>widths</code> and <code>densities</code> at the same time.</p>
</li>
<li>
<p><a href="">#17857</a> <a href=""><code>2637ed1</code></a> Thanks <a href="https://github.com/Princesseuh"><code>@​Princesseuh</code></a>! - Improves rendering performance</p>
</li>
<li>
<p><a href="">#17943</a> <a href=""><code>2fc7ce9</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes a WebAssembly error when importing <code>astro:actions</code> in tests that run under <code>@cloudflare/vitest-pool-workers</code></p>
</li>
<li>
<p><a href="">#18018</a> <a href=""><code>1b5a234</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes trailing-slash redirect response body pointing to the incoming URL instead of the redirect target. The <code>location</code> header was correct, but the HTML body (<code>&lt;meta http-equiv=&quot;refresh&quot;&gt;</code>, <code>&lt;title&gt;</code>, and <code>&lt;a&gt;</code> tag) contained the original request path without the trailing-slash correction or query string.</p>
</li>
<li>
<p><a href="">#17905</a> <a href=""><code>eaf70fa</code></a> Thanks <a href="https://github.com/SudoDevStudio"><code>@​SudoDevStudio</code></a>! - Fixes custom dev toolbar apps losing their UI after client-side navigation with <code>&lt;ClientRouter /&gt;</code>.</p>
</li>
<li>
<p><a href="">#18011</a> <a href=""><code>558b301</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes prerendered Cloudflare pages rendering as <code>[object Object]</code> when <code>nodejs_compat</code> is enabled in <code>wrangler.toml</code></p>
</li>
<li>
<p><a href="">#17944</a> <a href=""><code>ba08e35</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Fixes a regression in <code>astro dev</code> where writes outside the module graph (for example, <code>@astrojs/cloudflare</code>'s <code>.wrangler/state</code> files) invalidated the middleware on every request, causing repeated SSR reloads. Such writes no longer invalidate the middleware.</p>
</li>
<li>
<p><a href="">#17531</a> <a href=""><code>ae837db</code></a> Thanks <a href="https://github.com/danilloestrela"><code>@​danilloestrela</code></a>! - Updates <code>svgo</code> to <code>4.0.2</code> to resolve a security advisory</p>
</li>
<li>
<p><a href="">#17953</a> <a href=""><code>dbbf10e</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes a one-time page reload shortly after the first load on cold dev-server starts when a project has framework components imported from MDX content entries. MDX files are now included in the dev dependency pre-bundling scan, so their framework dependencies are bundled up front instead of being discovered (and reloaded for) at runtime.</p>
</li>
<li>
<p><a href="">#17955</a> <a href=""><code>4e8ad9a</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Improves dev server startup time. The content config and dev server app module graphs now begin compiling during server creation without blocking the server from listening. Request handling waits for the shared setup result when needed, cutting <code>astro dev</code> ready time by roughly a third on projects with a content config.</p>
</li>
<li>
<p><a href="">#17960</a> <a href=""><code>9838049</code></a> Thanks <a href="https://github.com/Chy-Zaber-Bin-Zahid"><code>@​Chy-Zaber-Bin-Zahid</code></a>! - Improves the diagnostics of some Astro errors.</p>
</li>
<li>
<p><a href="">#17998</a> <a href=""><code>0e5478d</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes SVG <code>&lt;style&gt;</code> elements nested inside <code>&lt;defs&gt;</code> or other container elements not being hashed for CSP</p>
</li>
<li>
<p><a href="">#17994</a> <a href=""><code>80f9f1d</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes <code>experimental.incrementalBuild</code> restoring pages with stale CSS after a preprocessor partial changes or missing original images referenced by restored pages</p>
</li>
<li>
<p><a href="">#17889</a> <a href=""><code>8ae6b46</code></a> Thanks <a href="https://github.com/ajfAfg"><code>@​ajfAfg</code></a>! - Fixes a bug where the dev server stripped the configured <code>base</code> from URLs that only share a prefix with it. With <code>base: '/s'</code>, requests to <code>/src/...</code> were rewritten to <code>/rc/...</code> and failed, breaking those pages during development.</p>
</li>
<li>
<p><a href="">#17980</a> <a href=""><code>cfccafa</code></a> Thanks <a href="https://github.com/gameroman"><code>@​gameroman</code></a>! - Improves JSDoc for fonts api</p>
</li>
<li>
<p><a href="">#17953</a> <a href=""><code>dbbf10e</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes CSS HMR for framework components rendered through content entries after <code>ClientRouter</code> navigation</p>
</li>
<li>
<p><a href="">#17970</a> <a href=""><code>0b4dc3a</code></a> Thanks <a href="https://github.com/matthewp"><code>@​matthewp</code></a>! - Improves serialization of transition animation values in generated CSS</p>
</li>
<li>
<p><a href="">#17999</a> <a href=""><code>30ef3cb</code></a> Thanks <a href="https://github.com/apps/astro-factory"><code>@​astro-factory</code></a>! - Fixes content collection HMR not updating prerendered pages when an adapter enables a separate prerender environment (e.g. <code>@astrojs/cloudflare</code> with <code>prerenderEnvironment: 'node'</code>)</p>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8a3106e</code></a> [ci] release (<a href="">#17939</a>)</li>
<li><a href=""><code>5efea1b</code></a> Add a version field to the astro-client-only fixture</li>
<li><a href=""><code>80f9f1d</code></a> Hash compiled CSS output in incremental build to detect Sass partial changes ...</li>
<li><a href=""><code>bc6572f</code></a> Revert &quot;Forward user class to Picture's outer element&quot; (<a href="">#18004</a>) (<a href="">#18030</a>)</li>
<li><a href=""><code>0e5478d</code></a> Normalize CRLF line endings before computing CSP hashes (<a href="">#17998</a>)</li>
<li><a href=""><code>30ef3cb</code></a> fix: invalidate prerender environment in invalidateDataStore (<a href="">#17991</a>) (<a href="">#17999</a>)</li>
<li><a href=""><code>312ab49</code></a> Fix redirect targets when a param value contains a <code>$</code> replacement pattern (#...</li>
<li><a href=""><code>1b5a234</code></a> Fix trailing-slash redirect body to match the Location header target (<a href="">#18018</a>)</li>
<li><a href=""><code>558b301</code></a> Fix prerendered Cloudflare pages rendering as [object Object] with nodejs_com...</li>
<li><a href=""><code>4464b3a</code></a> fix(assets): forward class to picture element in Picture component (<a href="">#18003</a>) (...</li>
<li>Additional commits viewable in <a href="https://github.com/withastro/astro/commits/astro@7.3.3/packages/astro">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `467924b8600a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.