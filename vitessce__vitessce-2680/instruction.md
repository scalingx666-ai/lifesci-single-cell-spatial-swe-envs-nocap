# Issue

**Title:** Make react a peer dependency of @vitessce/neuroglancer

## Description

#### Background
Downstream consumers fail to reconcile dependencies because `@vitessce/neuroglancer` requires exactly `react: "19.2.6"`.

`@vitessce/neuroglancer` listed `react` under `dependencies` as `catalog:`. At publish time pnpm replaces `catalog:` with the catalog value, so the published package required the exact pinned development version. All other published packages keep `react` in `devDependencies` (`catalog:`) and declare a range in `peerDependencies`. The bundle already externalizes React in `scripts/vite.config.mjs`, so only the package metadata needed to change.

#### Change List
- `packages/view-types/neuroglancer/package.json`: move `react` from `dependencies` to `devDependencies`, and add `peerDependencies.react: "^16.8.0 || ^17.0.0 || ^18.0.0 || ^19.0.0"` (same range as `@vitessce/vit-s` and the other view types; neuroglancer uses no React 18+ APIs).
- `pnpm-lock.yaml`: corresponding importer update.
- Changeset (patch) for `@vitessce/neuroglancer`.

Verified with `pnpm pack`: the packed `package.json` has no `react` in `dependencies` and has the peer range above. No other package under `packages/` lists `react` or `react-dom` in `dependencies`.

#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable
 - [x] New subpackage(s) manually published to NPM and trusted publishing enabled, or not applicable

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bb17a7616165`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.