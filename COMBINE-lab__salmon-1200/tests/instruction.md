# Issue

**Title:** ci(deps): bump docker/setup-buildx-action from 3 to 4

## Description

Bumps [docker/setup-buildx-action](https://github.com/docker/setup-buildx-action) from 3 to 4.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/setup-buildx-action/releases">docker/setup-buildx-action's releases</a>.</em></p>
<blockquote>
<h2>v4.0.0</h2>
<ul>
<li>Node 24 as default runtime (requires <a href="https://github.com/actions/runner/releases/tag/v2.327.1">Actions Runner v2.327.1</a> or later) by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#483</a></li>
<li>Remove deprecated inputs/outputs by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#464</a></li>
<li>Switch to ESM and update config/test wiring by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#481</a></li>
<li>Bump <code>@​actions/core</code> from 1.11.1 to 3.0.0 in <a href="">docker/setup-buildx-action#475</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.63.0 to 0.79.0 in <a href="">docker/setup-buildx-action#482</a> <a href="">docker/setup-buildx-action#485</a></li>
<li>Bump js-yaml from 4.1.0 to 4.1.1 in <a href="">docker/setup-buildx-action#452</a></li>
<li>Bump lodash from 4.17.21 to 4.17.23 in <a href="">docker/setup-buildx-action#472</a></li>
<li>Bump minimatch from 3.1.2 to 3.1.5 in <a href="">docker/setup-buildx-action#480</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v3.12.0...v4.0.0">https://github.com/docker/setup-buildx-action/compare/v3.12.0...v4.0.0</a></p>
<h2>v3.12.0</h2>
<ul>
<li>Deprecate <code>install</code> input by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#455</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.62.1 to 0.63.0 in <a href="">docker/setup-buildx-action#434</a></li>
<li>Bump brace-expansion from 1.1.11 to 1.1.12 in <a href="">docker/setup-buildx-action#436</a></li>
<li>Bump form-data from 2.5.1 to 2.5.5 in <a href="">docker/setup-buildx-action#432</a></li>
<li>Bump undici from 5.28.4 to 5.29.0 in <a href="">docker/setup-buildx-action#435</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v3.11.1...v3.12.0">https://github.com/docker/setup-buildx-action/compare/v3.11.1...v3.12.0</a></p>
<h2>v3.11.1</h2>
<ul>
<li>Fix <code>keep-state</code> not being respected by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#429</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v3.11.0...v3.11.1">https://github.com/docker/setup-buildx-action/compare/v3.11.0...v3.11.1</a></p>
<h2>v3.11.0</h2>
<ul>
<li>Keep BuildKit state support by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#427</a></li>
<li>Remove aliases created when installing by default by <a href="https://github.com/hashhar"><code>@​hashhar</code></a> in <a href="">docker/setup-buildx-action#139</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.56.0 to 0.62.1 in <a href="">docker/setup-buildx-action#422</a> <a href="">docker/setup-buildx-action#425</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v3.10.0...v3.11.0">https://github.com/docker/setup-buildx-action/compare/v3.10.0...v3.11.0</a></p>
<h2>v3.10.0</h2>
<ul>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.54.0 to 0.56.0 in <a href="">docker/setup-buildx-action#408</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v3.9.0...v3.10.0">https://github.com/docker/setup-buildx-action/compare/v3.9.0...v3.10.0</a></p>
<h2>v3.9.0</h2>
<ul>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.48.0 to 0.54.0 in <a href="">docker/setup-buildx-action#402</a> <a href="">docker/setup-buildx-action#404</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v3.8.0...v3.9.0">https://github.com/docker/setup-buildx-action/compare/v3.8.0...v3.9.0</a></p>
<h2>v3.8.0</h2>
<ul>
<li>Make cloud prefix optional to download buildx if driver is cloud by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-buildx-action#390</a></li>
<li>Bump <code>@​actions/core</code> from 1.10.1 to 1.11.1 in <a href="">docker/setup-buildx-action#370</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.39.0 to 0.48.0 in <a href="">docker/setup-buildx-action#389</a></li>
<li>Bump cross-spawn from 7.0.3 to 7.0.6 in <a href="">docker/setup-buildx-action#382</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-buildx-action/compare/v3.7.1...v3.8.0">https://github.com/docker/setup-buildx-action/compare/v3.7.1...v3.8.0</a></p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>37fe631</code></a> Merge pull request <a href="">#595</a> from docker/dependabot/npm_and_yarn/docker/actions-to...</li>
<li><a href=""><code>b5c4f91</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>3e93b63</code></a> build(deps): bump <code>@​docker/actions-toolkit</code> from 0.92.0 to 0.95.0</li>
<li><a href=""><code>e527031</code></a> Merge pull request <a href="">#600</a> from docker/dependabot/npm_and_yarn/brace-expansion-1...</li>
<li><a href=""><code>c68814b</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>3f891b0</code></a> build(deps): bump brace-expansion from 1.1.13 to 1.1.18</li>
<li><a href=""><code>787db26</code></a> Merge pull request <a href="">#585</a> from docker/dependabot/npm_and_yarn/js-yaml-5.2.1</li>
<li><a href=""><code>f779368</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>7d5e604</code></a> build(deps): bump js-yaml from 5.2.0 to 5.3.0</li>
<li><a href=""><code>292c2fb</code></a> Merge pull request <a href="">#590</a> from docker/dependabot/github_actions/actions/setup-n...</li>
<li>Additional commits viewable in <a href="https://github.com/docker/setup-buildx-action/compare/v3...v4">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=docker/setup-buildx-action&package-manager=github_actions&previous-version=3&new-version=4)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c81b42e94bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.