# Issue

**Title:** Publish JSON schema built with base plugins

## Description

## Summary

`@vitessce/json-schema` now also publishes `config-<latestVersion>.base-plugins.schema.json` (currently `config-1.0.18.base-plugins.schema.json`). It is generated with `zod-to-json-schema` from `buildConfigSchema(baseFileTypes, baseJointFileTypes, baseCoordinationTypes, baseViewTypes)`, which is the same schema `<Vitessce/>` uses to validate configs when no additional plugins are provided. Unlike the existing plugin-agnostic `config-<version>.schema.json` files, it checks file definition `fileType`/`options`, view `component` names, and coordination values.

## Implementation notes

- `base-plugins.ts` can't be imported in plain Node: it pulls in JSON imports, dependencies with broken ESM (e.g. `rc-tree`), and modules that touch `window` at import time (e.g. `higlass-register`). The script now runs with `vite-node`, which loads workspace sources the way vitest does, after setting up a minimal jsdom `window`/`document`.
- New devDependencies of `@vitessce/json-schema`: `@vitessce/all`, `jsdom`, `vite-node` (via a new catalog entry that resolves to the same 3.2.4 already used by vitest). These are devDependencies so that installing `@vitessce/json-schema` does not install all of Vitessce.
- `pnpm run build-json-schema` is added to the PR test workflow. Previously it only ran in the release workflow, so a breakage (e.g. a new view type that touches another DOM global at import time) would first surface on `main`.

## Validation

All 116 example configs from `@vitessce/example-configs` were upgraded to the latest version and validated with both the Zod schema and Python `jsonschema` (Draft 7) against the generated file:

- 112/116 agree.
- The remaining 4 pass Zod but fail the JSON schema because they contain option keys that Vitessce ignores (`region` in two spatialdata configs, `dimensions` in two neuroglancer configs). Zod strips unknown keys, while `zod-to-json-schema` emits `additionalProperties: false`. This matches the behavior of the existing published JSON schemas, and is arguably desirable for catching typos in generated configs. Mirroring Zod's strip behavior would require upgrading `zod-to-json-schema` (3.21.1 lacks `removeAdditionalStrategy`).
- Mutations of a valid config (unknown `fileType`, unknown `component`, unknown coordination type, wrong coordination value type, invalid view-level coordination value, invalid AnnData options) are all rejected.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88f64f6388b5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.