# Issue

**Title:** [DEPENDABOT]: Bump panel from 0.12.7 to 0.13.1

## Description

Bumps [panel](https://github.com/holoviz/panel) from 0.12.7 to 0.13.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/holoviz/panel/releases">panel's releases</a>.</em></p>
<blockquote>
<h2>Version 0.13.1</h2>
<p>This release is primarily a bug fix release but also includes a number of enhancements. Many thanks to <a href="https://github.com/Hoxbro"><code>@​Hoxbro</code></a>, <a href="https://github.com/joelostblom"><code>@​joelostblom</code></a>, <a href="https://github.com/raybellwaves"><code>@​raybellwaves</code></a>, <a href="https://github.com/pdrok"><code>@​pdrok</code></a>, <a href="https://github.com/tlvu"><code>@​tlvu</code></a>, <a href="https://github.com/govinda18"><code>@​govinda18</code></a>, <a href="https://github.com/MridulS"><code>@​MridulS</code></a> and the core maintainers <a href="https://github.com/MarcSkovMadsen"><code>@​MarcSkovMadsen</code></a>, <a href="https://github.com/maximlt"><code>@​maximlt</code></a> and <a href="https://github.com/philippjfr"><code>@​philippjfr</code></a> for contributing to this release.</p>
<h3>Enhancements</h3>
<ul>
<li>Add repr to cell and edit events (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3534">#3434</a>)</li>
<li>Improvements for pyodide handling (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3444">#3444</a>, <a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3508">#3508</a>, <a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3511">#3511</a>)</li>
<li>Add support for <code>Plotly</code> animation frames (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3499">#3449</a>)</li>
<li>Implement single and multi-selection in Vega pane (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3470">#3470</a>, <a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3499">#3499</a>, <a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3505">#3505</a>)</li>
<li>Add typehints to help developers and users (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3476">#3476</a>)</li>
<li>Add <code>pn.state.execute</code> method to run callbacks in the right context (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3550">#3550</a>)</li>
<li>Add support for asynchronous <code>on_edit</code>/<code>on_click</code> Tabulator callbacks (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3550">#3550</a>)</li>
<li>Add <code>DatetimeRangeSlider</code> widget (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3548">#3548</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>Fix pyodide array buffer conversion (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3409">#3409</a>)</li>
<li>Allow <code>placeholder</code> to be updated on <code>TextEditor</code> (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3427">#3427</a>)</li>
<li>Fix issues editing data in sorted columns (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3431">#3431</a>)</li>
<li>Ensure bokeh correctly detects whether <code>HTML</code>/<code>Markdown</code> contains latex (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3438">#3438</a>)</li>
<li>Ensure notifications work on server created with <code>pn.serve</code> and <code>.show</code> (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3445">#3445</a>)</li>
<li>Replace slickgrid background image in custom <code>FastTemplate</code> CSS (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3461">#3461</a>)</li>
<li>Ensure <code>param.Array</code> is synced correctly in <code>ReactiveHTML</code> (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3456">#3456</a>)</li>
<li>Ensure selection on filtered <code>Tabulator</code> does not raise out-of-bounds error (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3462">#3462</a>)</li>
<li>Ensure updating <code>Tabulator</code> does not reset scroll position (<a href="https://github-redirect.dependabot.com/holoviz/panel/issues/3450">#3450</a>)</li>
<li>Various fixes for <code>FastTemplate</code> CSS (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3464">#3464</a>)</li>
<li>Ensure <code>Tabulator</code> <code>on_click</code> and <code>on_edit</code> events return correct row when paginated (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3410">#3410</a>)</li>
<li>Fix broken JupyterLab preview (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3469">#3469</a>)</li>
<li>Skip <code>Tabulator</code> row selection when clicking on expand button (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3474">#3474</a>)</li>
<li>Ensure overflow in <code>MaterialTemplate</code> is not clipped (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3492">#3492</a>)</li>
<li>Allow providing <code>--index</code> for directory style apps (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3493">#3493</a>)</li>
<li>Ensure Tabulator expanded rows are sized correctly after re-render (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3507">#3507</a>)</li>
<li>Make CodeHandler robust to document that has been destroyed (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3510">#3510</a>)</li>
<li>Do not sync <code>DataFrame</code> widget <code>sorters</code> parameter with bokeh model (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3527">#3527</a>)</li>
<li>Ensure that HoloViews callback events are not auto-dispatched (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3528">#3528</a>)</li>
<li>Ensure non-updateable <code>Pane</code> can be updated inside <code>Tabs</code> (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3532">#3532</a>)</li>
<li>Fix slowdown of JupyterLab on Windows (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3431">#3531</a>)</li>
<li>Fix issue with inverted data when editing a cell in a sorted Tabulator column (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3531">#3531</a>)</li>
<li>Ensure <code>Tabulator</code> has correct layout after re-render (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3536">#3536</a>)</li>
<li>Do not log events generated by admin page on the admin page (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3539">#3539</a>)</li>
<li>Fix Tabulator events when the original column is not a string (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3541">#3541</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Adds docstrings to layouts (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3417">#3417</a>)</li>
<li>Show how to filter categorical and temporal data from <code>Altair</code>/VegaLite (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3401">#3401</a>)</li>
<li>Document how to make a <code>Tabulator</code> column non-editable (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3489">#3489</a>)</li>
</ul>
<h2>Version 0.13.0</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/holoviz/panel/blob/master/CHANGELOG.md">panel's changelog</a>.</em></p>
<blockquote>
<h2>Version 0.13.1</h2>
<p>Date: 2022-05-20</p>
<h3>Enhancements</h3>
<ul>
<li>Add repr to cell and edit events (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3534">#3434</a>)</li>
<li>Improvements for pyodide handling (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3444">#3444</a>, <a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3508">#3508</a>, <a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3511">#3511</a>)</li>
<li>Add support for <code>Plotly</code> animation frames (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3499">#3449</a>)</li>
<li>Implement single and multi-selection in Vega pane (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3470">#3470</a>, <a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3499">#3499</a>, <a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3505">#3505</a>)</li>
<li>Add typehints to help developers and users (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3476">#3476</a>)</li>
<li>Add <code>pn.state.execute</code> method to run callbacks in the right context (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3550">#3550</a>)</li>
<li>Add support for asynchronous <code>on_edit</code>/<code>on_click</code> Tabulator callbacks (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3550">#3550</a>)</li>
<li>Add <code>DatetimeRangeSlider</code> widget (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3548">#3548</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>Fix pyodide array buffer conversion (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3409">#3409</a>)</li>
<li>Allow <code>placeholder</code> to be updated on <code>TextEditor</code> (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3427">#3427</a>)</li>
<li>Fix issues editing data in sorted columns (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3431">#3431</a>)</li>
<li>Ensure bokeh correctly detects whether <code>HTML</code>/<code>Markdown</code> contains latex (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3438">#3438</a>)</li>
<li>Ensure notifications work on server created with <code>pn.serve</code> and <code>.show</code> (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3445">#3445</a>)</li>
<li>Replace slickgrid background image in custom <code>FastTemplate</code> CSS (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3461">#3461</a>)</li>
<li>Ensure <code>param.Array</code> is synced correctly in <code>ReactiveHTML</code> (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3456">#3456</a>)</li>
<li>Ensure selection on filtered <code>Tabulator</code> does not raise out-of-bounds error (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3462">#3462</a>)</li>
<li>Ensure updating <code>Tabulator</code> does not reset scroll position (<a href="https://github-redirect.dependabot.com/holoviz/panel/issues/3450">#3450</a>)</li>
<li>Various fixes for <code>FastTemplate</code> CSS (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3464">#3464</a>)</li>
<li>Ensure <code>Tabulator</code> <code>on_click</code> and <code>on_edit</code> events return correct row when paginated (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3410">#3410</a>)</li>
<li>Fix broken JupyterLab preview (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3469">#3469</a>)</li>
<li>Skip <code>Tabulator</code> row selection when clicking on expand button (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3474">#3474</a>)</li>
<li>Ensure overflow in <code>MaterialTemplate</code> is not clipped (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3492">#3492</a>)</li>
<li>Allow providing <code>--index</code> for directory style apps (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3493">#3493</a>)</li>
<li>Ensure Tabulator expanded rows are sized correctly after re-render (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3507">#3507</a>)</li>
<li>Make CodeHandler robust to document that has been destroyed (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3510">#3510</a>)</li>
<li>Do not sync <code>DataFrame</code> widget <code>sorters</code> parameter with bokeh model (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3527">#3527</a>)</li>
<li>Ensure that HoloViews callback events are not auto-dispatched (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3528">#3528</a>)</li>
<li>Ensure non-updateable <code>Pane</code> can be updated inside <code>Tabs</code> (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3532">#3532</a>)</li>
<li>Fix slowdown of JupyterLab on Windows (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3431">#3531</a>)</li>
<li>Fix issue with inverted data when editing a cell in a sorted Tabulator column (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3531">#3531</a>)</li>
<li>Ensure <code>Tabulator</code> has correct layout after re-render (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3536">#3536</a>)</li>
<li>Do not log events generated by admin page on the admin page (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3539">#3539</a>)</li>
<li>Fix Tabulator events when the original column is not a string (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3541">#3541</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Adds docstrings to layouts (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3417">#3417</a>)</li>
<li>Show how to filter categorical and temporal data from <code>Altair</code>/VegaLite (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3401">#3401</a>)</li>
<li>Document how to make a <code>Tabulator</code> column non-editable (<a href="https://github-redirect.dependabot.com/holoviz/panel/pull/3489">#3489</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>bdf0b25</code></a> Bump panel.js version to 0.13.1</li>
<li><a href=""><code>346278c</code></a> Ensure Tabulator expand icon updates on click (<a href="https://github-redirect.dependabot.com/holoviz/panel/issues/3554">#3554</a>)</li>
<li><a href=""><code>0161763</code></a> Add <code>execute</code> method to run callbacks and add support to asynchronous `on_edi...</li>
<li><a href=""><code>1a168b5</code></a> Fix styling offset for Tabulator (<a href="https://github-redirect.dependabot.com/holoviz/panel/issues/3551">#3551</a>)</li>
<li><a href=""><code>0dab3ba</code></a> Use DatetimeRangeSlider for param.DateRange mapping (<a href="https://github-redirect.dependabot.com/holoviz/panel/issues/3549">#3549</a>)</li>
<li><a href=""><code>c6f728f</code></a> Add DatetimeRangeSlider (<a href="https://github-redirect.dependabot.com/holoviz/panel/issues/3548">#3548</a>)</li>
<li><a href=""><code>c00f5c1</code></a> Bump panel.js version to 0.13.1rc3</li>
<li><a href=""><code>02e5e7b</code></a> Swap index page example</li>
<li><a href=""><code>7687d59</code></a> Add warnings when function without dependencies is passed to ParamFunction (#...</li>
<li><a href=""><code>b6815b2</code></a> Fix Tabulator regressions related to frozen columns (<a href="https://github-redirect.dependabot.com/holoviz/panel/issues/3544">#3544</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/holoviz/panel/compare/v0.12.7...v0.13.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=panel&package-manager=pip&previous-version=0.12.7&new-version=0.13.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ff1e24c0a74`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.