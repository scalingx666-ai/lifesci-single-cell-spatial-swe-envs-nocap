# Issue

**Title:** chore(deps-dev): bump pre-commit from 4.6.0 to 4.6.1 in the development-dependencies group across 1 directory

## Description

Bumps the development-dependencies group with 1 update in the / directory: [pre-commit](https://github.com/pre-commit/pre-commit).

Updates `pre-commit` from 4.6.0 to 4.6.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pre-commit/pre-commit/releases">pre-commit's releases</a>.</em></p>
<blockquote>
<h2>pre-commit v4.6.1</h2>
<h3>Fixes</h3>
<ul>
<li>Install <code>language: node</code> hooks via <code>git</code>.
<ul>
<li>Fixes npm 12.x compatibility</li>
<li><a href="">#3719</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
<li><a href="">#3517</a> issue by <a href="https://github.com/ojob"><code>@​ojob</code></a>.</li>
</ul>
</li>
<li>Set <code>JULIA_DEPOT_PATH</code> for <code>language: julia</code>.
<ul>
<li><a href="">#3711</a> PR by <a href="https://github.com/damonbayer"><code>@​damonbayer</code></a>.</li>
<li><a href="">pre-commit-ci/runner-image#335</a> issue by <a href="https://github.com/damonbayer"><code>@​damonbayer</code></a>.</li>
</ul>
</li>
<li>Produce error on mistyped <code>--repo</code> for <code>pre-commit autoupdate</code>.
<ul>
<li><a href="">#3701</a> PR by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
<li><a href="">#3695</a> issue by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
</ul>
</li>
<li>Improve performance of commit existence check in <code>pre-push</code>.
<ul>
<li><a href="">#3726</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
<li><a href="">#3604</a> issue by <a href="https://github.com/ptarjan"><code>@​ptarjan</code></a>.</li>
</ul>
</li>
<li>Avoid duplicating conflicted filenames during <code>pre-commit run --all-files</code>.
<ul>
<li><a href="">#3727</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
<li><a href="">#3706</a> issue by <a href="https://github.com/RomanValov"><code>@​RomanValov</code></a>.</li>
</ul>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pre-commit/pre-commit/blob/main/CHANGELOG.md">pre-commit's changelog</a>.</em></p>
<blockquote>
<h1>4.6.1 - 2026-07-21</h1>
<h3>Fixes</h3>
<ul>
<li>Install <code>language: node</code> hooks via <code>git</code>.
<ul>
<li>Fixes npm 12.x compatibility</li>
<li><a href="">#3719</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
<li><a href="">#3517</a> issue by <a href="https://github.com/ojob"><code>@​ojob</code></a>.</li>
</ul>
</li>
<li>Set <code>JULIA_DEPOT_PATH</code> for <code>language: julia</code>.
<ul>
<li><a href="">#3711</a> PR by <a href="https://github.com/damonbayer"><code>@​damonbayer</code></a>.</li>
<li><a href="">pre-commit-ci/runner-image#335</a> issue by <a href="https://github.com/damonbayer"><code>@​damonbayer</code></a>.</li>
</ul>
</li>
<li>Produce error on mistyped <code>--repo</code> for <code>pre-commit autoupdate</code>.
<ul>
<li><a href="">#3701</a> PR by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
<li><a href="">#3695</a> issue by <a href="https://github.com/mxr"><code>@​mxr</code></a>.</li>
</ul>
</li>
<li>Improve performance of commit existence check in <code>pre-push</code>.
<ul>
<li><a href="">#3726</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
<li><a href="">#3604</a> issue by <a href="https://github.com/ptarjan"><code>@​ptarjan</code></a>.</li>
</ul>
</li>
<li>Avoid duplicating conflicted filenames during <code>pre-commit run --all-files</code>.
<ul>
<li><a href="">#3727</a> PR by <a href="https://github.com/asottile"><code>@​asottile</code></a>.</li>
<li><a href="">#3706</a> issue by <a href="https://github.com/RomanValov"><code>@​RomanValov</code></a>.</li>
</ul>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>242ce8a</code></a> v4.6.1</li>
<li><a href=""><code>766e550</code></a> Merge pull request <a href="">#3727</a> from pre-commit/dedupe</li>
<li><a href=""><code>1558d06</code></a> Merge pull request <a href="">#3726</a> from pre-commit/exists-faster</li>
<li><a href=""><code>8a1c47a</code></a> avoid duplicate files in --all-files during conflict</li>
<li><a href=""><code>2e01c99</code></a> faster check of rev existing locally as a commit</li>
<li><a href=""><code>3613bf2</code></a> Merge pull request <a href="">#3701</a> from pre-commit/autoupdate-repos</li>
<li><a href=""><code>1d811d9</code></a> Return an error for invalid --repo</li>
<li><a href=""><code>374d354</code></a> Merge pull request <a href="">#3711</a> from damonbayer/dmb_JULIA_DEPOT_PATH</li>
<li><a href=""><code>1e7994f</code></a> set JULIA_DEPOT_PATH</li>
<li><a href=""><code>b2b9119</code></a> Merge pull request <a href="">#3719</a> from pre-commit/npm-unknown-options</li>
<li>Additional commits viewable in <a href="https://github.com/pre-commit/pre-commit/compare/v4.6.0...v4.6.1">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `654d0041390e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.