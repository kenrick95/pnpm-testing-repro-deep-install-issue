# Repro

## Description

- `@kenrick95/internal-g` has dependency on `@kenrick95/external-depend-on-internal-dep` (external package)
- `@kenrick95/external-depend-on-internal-dep` has dependency on `@kenrick95/internal-f` 
- Workspace setting `link-workspace-packages = deep` causes `@kenrick95/external-depend-on-internal-dep` to use the internally linked version instead of downloaded from registry
- **However** when a filtered install occurred to `@kenrick95/internal-g` (with "`<pkg_name>...`", meaning to select package and its dependencies _(direct and non-direct)_), `@kenrick95/internal-f`'s dependencies are not installed!

## Run

1. Clear all node_modules
```
pnpm run clean
```
2. Run filtered install
```
pnpm --filter "@kenrick95/internal-g..." install
```
3. Notice that `packages/g/node_modules` exist but `packages/f/node_modules` does not exist!
