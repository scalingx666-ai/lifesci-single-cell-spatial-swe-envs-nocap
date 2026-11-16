# Issue

**Title:** [DEPENDABOT]: Bump rich from 9.13.0 to 10.0.1

## Description

Bumps [rich](https://github.com/willmcgugan/rich) from 9.13.0 to 10.0.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/releases">rich's releases</a>.</em></p>
<blockquote>
<h2>Fix for race condition in Progress</h2>
<h2>[10.0.1] - 2021-03-30</h2>
<h3>Fixed</h3>
<ul>
<li>Fixed race condition that duplicated lines in progress <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1144">willmcgugan/rich#1144</a></li>
</ul>
<h2>Update to render protocol</h2>
<p>Some significant signature to render protocol, hence the major version bump. These are unlikely to impact many people unless you are implementing your own renderables.</p>
<p>Most of the work in this version was to aid development of adding more dynamic features to future versions.</p>
<p>See changelog for details...</p>
<h2>[10.0.0] - 2021-03-27</h2>
<h3>Changed</h3>
<ul>
<li>Made pydoc import lazy as at least one use found it slow to import <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1104">willmcgugan/rich#1104</a></li>
<li>Modified string highlighting to not match in the middle of a word, so that apostrophes are not considered strings</li>
<li>New way of encoding control codes in Segment</li>
<li>New signature for Control class</li>
<li>Changed Layout.split to use new Splitter class</li>
<li>Improved layout.tree</li>
<li>Changed default theme color for repr.number to cyan</li>
<li><code>__rich_measure__</code> signature changed to accept ConsoleOptions rather than max_width</li>
</ul>
<h3>Added</h3>
<ul>
<li>Added <code>__rich_repr__</code> protocol method to Pretty</li>
<li>Added rich.region.Region</li>
<li>Added ConsoleOptions.update_dimensions</li>
<li>Added rich.console.ScreenUpdate</li>
<li>Added Console.is_alt_screen</li>
<li>Added Control.segment, Control.bell, Control.home, Control.move_to, Control.clear, Control.show_cursor, Control.alt_screen</li>
<li>Added Console.update_screen and Console.update_screen_lines</li>
<li>Added Layout.add_split, Layout.split_column, Layout.split_row, layout.refresh</li>
<li>Added new Rich repr protocol <code>__rich_repr__</code></li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed table style taking precedence over row style <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1129">willmcgugan/rich#1129</a></li>
<li>Fixed incorrect measurement of Text with new lines and whitespace <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1133">willmcgugan/rich#1133</a></li>
<li>Made type annotations consistent for various <code>total</code> keyword arguments in <code>rich.progress</code> and rich.<code>progress_bar</code></li>
<li>Disabled Progress no longer displays itself when starting <a href="https://github-redirect.dependabot.com/willmcgugan/rich/pull/1125">willmcgugan/rich#1125</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/blob/master/CHANGELOG.md">rich's changelog</a>.</em></p>
<blockquote>
<h2>[10.0.1] - 2021-03-30</h2>
<h3>Fixed</h3>
<ul>
<li>Fixed race condition that duplicated lines in progress <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1144">willmcgugan/rich#1144</a></li>
</ul>
<h2>[10.0.0] - 2021-03-27</h2>
<h3>Changed</h3>
<ul>
<li>Made pydoc import lazy as at least one use found it slow to import <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1104">willmcgugan/rich#1104</a></li>
<li>Modified string highlighting to not match in the middle of a word, so that apostrophes are not considered strings</li>
<li>New way of encoding control codes in Segment</li>
<li>New signature for Control class</li>
<li>Changed Layout.split to use new Splitter class</li>
<li>Improved layout.tree</li>
<li>Changed default theme color for repr.number to cyan</li>
<li><code>__rich_measure__</code> signature changed to accept ConsoleOptions rather than max_width</li>
</ul>
<h3>Added</h3>
<ul>
<li>Added <code>__rich_repr__</code> protocol method to Pretty</li>
<li>Added rich.region.Region</li>
<li>Added ConsoleOptions.update_dimensions</li>
<li>Added rich.console.ScreenUpdate</li>
<li>Added Console.is_alt_screen</li>
<li>Added Control.segment, Control.bell, Control.home, Control.move_to, Control.clear, Control.show_cursor, Control.alt_screen</li>
<li>Added Console.update_screen and Console.update_screen_lines</li>
<li>Added Layout.add_split, Layout.split_column, Layout.split_row, layout.refresh</li>
<li>Added new Rich repr protocol <code>__rich_repr__</code></li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed table style taking precedence over row style <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1129">willmcgugan/rich#1129</a></li>
<li>Fixed incorrect measurement of Text with new lines and whitespace <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1133">willmcgugan/rich#1133</a></li>
<li>Made type annotations consistent for various <code>total</code> keyword arguments in <code>rich.progress</code> and rich.<code>progress_bar</code></li>
<li>Disabled Progress no longer displays itself when starting <a href="https://github-redirect.dependabot.com/willmcgugan/rich/pull/1125">willmcgugan/rich#1125</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>11c305e</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1146">#1146</a> from willmcgugan/progress-race-condition</li>
<li><a href=""><code>bcb2923</code></a> version bump</li>
<li><a href=""><code>23497ed</code></a> fix for race condition</li>
<li><a href=""><code>0758f2e</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1142">#1142</a> from apoclyps/layout-example-using-splitter</li>
<li><a href=""><code>f24b668</code></a> Updates example/layout.py to use Splitter class</li>
<li><a href=""><code>57736f4</code></a> typo in requirements</li>
<li><a href=""><code>7dd46be</code></a> spelling in readme</li>
<li><a href=""><code>76073ba</code></a> add copybutton to docs</li>
<li><a href=""><code>a28cf3a</code></a> doc fix</li>
<li><a href=""><code>e4d5eda</code></a> Update progress.rst</li>
<li>Additional commits viewable in <a href="https://github.com/willmcgugan/rich/compare/v9.13.0...v10.0.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rich&package-manager=pip&previous-version=9.13.0&new-version=10.0.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `00db76114f1c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.