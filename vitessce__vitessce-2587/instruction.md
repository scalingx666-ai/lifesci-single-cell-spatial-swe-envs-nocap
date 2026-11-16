# Issue

**Title:** NickAkhmetov/Fix 2586 - catch module-scope evaluation of optional xr dependencies

## Description

#### Background

`@react-three/xr` is an optional peer dependency of `@vitessce/spatial-three`. To keep the package buildable when that peer is absent, `xr/xrModule.ts` holds it behind a single dynamic namespace import in a module-level `let`, populated by `loadXRModule()` and read back by `getXRModule()`, which throws until the load resolves. That indirection landed in 4.0.1 (#2525) and fixed the missing-peer consumer build failure, but it introduced a subtler one: five modules called `getXRModule()` at module scope, so their correctness depended on the consuming application's bundler chunking rather than on anything this package controls.

`SpatialWrapper` awaits `loadXRModule()` in an effect and only then renders the `React.lazy` wrappers, so the intended ordering is sound in source. But "lazy-loaded" is a property of the emitted chunk graph, not of the source layout. When a consumer's bundler folds those modules into an eagerly-evaluated chunk, page load throws before any React component mounts:

```
Uncaught Error: @react-three/xr is not loaded; call loadXRModule() first.
```

This was reported from [hubmapconsortium/portal-ui](https://github.com/hubmapconsortium/portal-ui) upgrading 4.0.0 → 4.0.6. Their Vite build has a `manualChunks(id)` rule putting everything under `/node_modules/` into one `vendors` chunk. `manualChunks` wins over dynamic-import chunk boundaries, so `xrStore-*.js`, `XRWrapper-*.js`, `XRSceneComponents-*.js`, `XREnterButton-*.js` and `GeometryAndMeshXR-*.js` all landed in the eager vendor bundle, `xrStore.ts` evaluated at page load, and it took down the whole application — all 25 of their page-load Cypress specs failed, including specs that never render a spatial view. The same hazard applies to Rollup-based Vite and to Webpack `splitChunks` configs that group all of `node_modules`.

The fix defers every `getXRModule()` call to call time, so evaluation order stops mattering and no consumer chunking strategy can break it. The lazy-loading and optional-peer scheme are otherwise unchanged.

#### Change List

- `xr/xrStore.ts`: replaced the module-scope `xrStore` const with a lazily-created, memoized `getXrStore()`. The type-only `import type { XRStore }` is kept as-is — dropping the `type` keyword there would break the optional-peer scheme.
- `xr/XRWrapper.tsx`: `const { XR } = getXRModule()` moved into the component body; `store={xrStore}` → `store={getXrStore()}`.
- `xr/XREnterButton.tsx`: three `xrStore.` references → `getXrStore().`. All three were already inside an effect or a click handler.
- `xr/HandDecorate.ts`, `xr/HandBbox.tsx`, `GeometryAndMeshXR.tsx`: module-scope `getXRModule()` destructures moved to the first line of each component body. The hooks are still called unconditionally on every render of components that only render after `loadXRModule()` has resolved, so rules-of-hooks stays satisfied.
- `xr/xrModule.ts`: reworded the constraint above `getXRModule()` to "Never call at module scope", naming Vite `manualChunks` / Webpack `splitChunks` as the reason. The previous wording ("only call from modules that are lazy-loaded") read as satisfied by the source layout when it actually depended on the consumer's build.
- `xr/module-scope.test.ts` (new): the test's static imports are the assertion — it imports all six XR modules and never calls `loadXRModule()`, so a reintroduced module-scope call fails at import. Verified it catches the regression: temporarily restoring one destructure fails with `Error: @react-three/xr is not loaded; call loadXRModule() first.` at `src/xr/HandBbox.tsx:7`.
- Changeset: `@vitessce/spatial-three` patch.
- `scripts/consumer-install.sh`: pinned the simulated consumer's react to the exact version the monorepo builds against, read from the monorepo's own installed react (the `catalog:` pin in `pnpm-workspace.yaml`, currently 19.2.6) and installed with `--save-exact`. Unrelated to the XR fix, but it was failing `test-e2e-html` on this branch and on `main`: the script installed `react@^19.0.0`, react 19.3.0 was published 2026-09-09, and `@react-three/fiber@9.7.0` declares peer `react ">=19 <19.3"`, so the install died with `ERESOLVE`. Verified locally that the pin resolves cleanly through the fiber/drei/xr, vite@7 and next@16 installs.

Also verified on the bundled output: after `vite build`, every `getXRModule()` call in the emitted `dist/` chunks sits inside a function body (`function XRWrapper`, `function HandBbox`, `function HandDecorate`, `function GeometryAndMeshXR`, `getXrStore`), and the chunk split is unchanged.

Consumers currently working around this by excluding the XR chunks from their vendor chunk can drop that exclusion once this ships; it hardcodes Vitessce's internal `dist` chunk names, which are Rollup defaults and not a stable interface.

#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49b8bbf76981`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.