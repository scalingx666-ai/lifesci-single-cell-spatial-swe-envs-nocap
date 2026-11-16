# Issue

**Title:** [DEPENDABOT]: Bump matplotlib from 3.3.4 to 3.4.1

## Description

Bumps [matplotlib](https://github.com/matplotlib/matplotlib) from 3.3.4 to 3.4.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/matplotlib/matplotlib/releases">matplotlib's releases</a>.</em></p>
<blockquote>
<h2>REL: v3.4.1</h2>
<p>This is the first bugfix release of the 3.4.x series.</p>
<p>This release contains several critical bug-fixes:</p>
<ul>
<li>fix errorbar when specifying fillstyle</li>
<li>fix Inkscape cleanup at exit on Windows for tests</li>
<li>fix legends of colour-mapped scatter plots</li>
<li>fix positioning of annotation fancy arrows</li>
<li>fix size and color rendering for 3D scatter plots</li>
<li>fix suptitle manual positioning when using constrained layout</li>
<li>respect antialiasing settings in cairo backends as well</li>
</ul>
<h2>REL: v3.4.0</h2>
<p>Highlights of this release include:</p>
<ul>
<li>Figure and Axes creation / management
<ul>
<li>New subfigure functionality</li>
<li>Single-line string notation for <code>subplot_mosaic</code></li>
<li>Changes to behavior of Axes creation methods (<code>gca</code>, <code>add_axes</code>, <code>add_subplot</code>)</li>
<li><code>add_subplot</code>/<code>add_axes</code> gained an <em>axes_class</em> parameter</li>
<li>Subplot and subplot2grid can now work with constrained layout</li>
</ul>
</li>
<li>Plotting methods
<ul>
<li><code>axline</code> supports transform parameter</li>
<li>New automatic labeling for bar charts</li>
<li>A list of hatches can be specified to <code>bar</code> and <code>barh</code></li>
<li>Setting <code>BarContainer</code> orientation</li>
<li>Contour plots now default to using <code>ScalarFormatter</code></li>
<li><code>Axes.errorbar</code> cycles non-color properties correctly</li>
<li><code>errorbar</code> <em>errorevery</em> parameter matches <em>markevery</em></li>
<li><code>hexbin</code> supports data reference for <em>C</em> parameter</li>
<li>Support callable for formatting of Sankey labels</li>
<li><code>Axes.spines</code> access shortcuts</li>
<li>New <code>stairs</code> method and <code>StepPatch</code> artist</li>
<li>Added <em>orientation</em> parameter for stem plots</li>
<li>Angles on Bracket arrow styles</li>
<li><code>TickedStroke</code> patheffect</li>
</ul>
</li>
<li>Colors and colormaps
<ul>
<li>Collection color specification and mapping</li>
<li>Transparency (alpha) can be set as an array in collections</li>
<li>pcolormesh has improved transparency handling by enabling snapping</li>
<li>IPython representations for Colormap objects</li>
<li><code>Colormap.set_extremes</code> and <code>Colormap.with_extremes</code></li>
<li>Get under/over/bad colors of Colormap objects</li>
<li>New <code>cm.unregister_cmap</code> function</li>
<li>New <code>CenteredNorm</code> for symmetrical data around a center</li>
<li>New <code>FuncNorm</code> for arbitrary normalizations</li>
<li>GridSpec-based colorbars can now be positioned above or to the left of the main axes</li>
</ul>
</li>
<li>Titles, ticks, and labels
<ul>
<li>supxlabel and supylabel</li>
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
<li><a href=""><code>223c30a</code></a> REL: v3.4.1</li>
<li><a href=""><code>cc45fb9</code></a> DOC: Update GitHub stats for 3.4.1.</li>
<li><a href=""><code>1748e33</code></a> Merge branch 'v3.4.0-doc' into v3.4.x</li>
<li><a href=""><code>17b3aa0</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/matplotlib/matplotlib/issues/19834">#19834</a> from QuLogic/backport-19812</li>
<li><a href=""><code>92a59fd</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/matplotlib/matplotlib/issues/19833">#19833</a> from meeseeksmachine/auto-backport-of-pr-19811-on-v...</li>
<li><a href=""><code>040649d</code></a> Backport PR <a href="https://github-redirect.dependabot.com/matplotlib/matplotlib/issues/19812">#19812</a>: FIX: size and color rendering for Path3DCollection</li>
<li><a href=""><code>6e6fcf4</code></a> Backport PR <a href="https://github-redirect.dependabot.com/matplotlib/matplotlib/issues/19811">#19811</a>: Fix Inkscape cleanup at exit on Windows.</li>
<li><a href=""><code>6547ba2</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/matplotlib/matplotlib/issues/19816">#19816</a> from QuLogic/fix-scatter-legend</li>
<li><a href=""><code>3bfe69c</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/matplotlib/matplotlib/issues/19830">#19830</a> from meeseeksmachine/auto-backport-of-pr-19824-on-v...</li>
<li><a href=""><code>ebc9277</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/matplotlib/matplotlib/issues/19829">#19829</a> from meeseeksmachine/auto-backport-of-pr-19822-on-v...</li>
<li>Additional commits viewable in <a href="https://github.com/matplotlib/matplotlib/compare/v3.3.4...v3.4.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=matplotlib&package-manager=pip&previous-version=3.3.4&new-version=3.4.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f3620506b633`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.