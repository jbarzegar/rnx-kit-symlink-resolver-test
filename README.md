# Running symlink resolver with pnpm (no extra configuration)

### Info:

```
node version: v16.14.0
pnpm version: 6.32.2 and tried 7
```

## Starting the app

Install deps with `pnpm install`

Start RN's dev server with: `pnpm start` results in the process crashing with this error:

```
error Cannot find module 'metro-resolver'. This probably means that '@rnx-kit/metro-resolver-symlinks' is not compatible with the version of 'metro' that you are currently using. Please update to the latest version and try again. If the issue still persists after the update, please file a bug at https://github.com/microsoft/rnx-kit/issues.
Error: Cannot find module 'metro-resolver'. This probably means that '@rnx-kit/metro-resolver-symlinks' is not compatible with the version of 'metro' that you are currently using. Please update to the latest version and try again. If the issue still persists after the update, please file a bug at https://github.com/microsoft/rnx-kit/issues.
    at getMetroResolver (/Users/james/Dev/jbarzegar/RnxKitTest/node_modules/.pnpm/@rnx-kit+metro-resolver-symlinks@0.1.19/node_modules/@rnx-kit/metro-resolver-symlinks/lib/resolver.js:50:15)
    at makeResolver (/Users/james/Dev/jbarzegar/RnxKitTest/node_modules/.pnpm/@rnx-kit+metro-resolver-symlinks@0.1.19/node_modules/@rnx-kit/metro-resolver-symlinks/lib/symlinkResolver.js:8:59)
    at Object.<anonymous> (/Users/james/Dev/jbarzegar/RnxKitTest/metro.config.js:14:21)
    at Module._compile (node:internal/modules/cjs/loader:1103:14)
    at Object.Module._extensions..js (node:internal/modules/cjs/loader:1155:10)
    at Module.load (node:internal/modules/cjs/loader:981:32)
    at Function.Module._load (node:internal/modules/cjs/loader:822:12)
    at Module.require (node:internal/modules/cjs/loader:1005:19)
    at require (node:internal/modules/cjs/helpers:102:18)
    at module.exports (/Users/james/Dev/jbarzegar/RnxKitTest/node_modules/.pnpm/import-fresh@2.0.0/node_modules/import-fresh/index.js:28:9)
info Run CLI with --verbose flag for more details.
 ELIFECYCLE  Command failed with exit code 1.
[1]
```

Ran `pnpm exec rnx-dep-check` ran without issue but returned a slew of warnings about packages that could not be resolved:

```
warn Unable to resolve module 'loose-envify'
warn Unable to resolve module 'object-assign'
warn Unable to resolve module '@jest/create-cache-key-function'
warn Unable to resolve module '@react-native-community/cli'
warn Unable to resolve module '@react-native-community/cli-tools'
warn Unable to resolve module 'chalk'
warn Unable to resolve module 'execa'
warn Unable to resolve module 'fs-extra'
warn Unable to resolve module 'glob'
warn Unable to resolve module 'jetifier'
warn Unable to resolve module 'lodash'
warn Unable to resolve module 'logkitty'
warn Unable to resolve module 'slash'
warn Unable to resolve module 'js-yaml'
warn Unable to resolve module 'ora'
warn Unable to resolve module 'plist'
warn Unable to resolve module '@react-native/assets'
warn Unable to resolve module '@react-native/normalize-color'
warn Unable to resolve module '@react-native/polyfills'
warn Unable to resolve module 'abort-controller'
warn Unable to resolve module 'anser'
warn Unable to resolve module 'base64-js'
warn Unable to resolve module 'invariant'
warn Unable to resolve module 'react-is'
warn Unable to resolve module 'event-target-shim'
warn Unable to resolve module 'hermes-engine'
warn Unable to resolve module 'jsc-android'
warn Unable to resolve module 'metro-react-native-babel-transformer'
warn Unable to resolve module 'metro-runtime'
warn Unable to resolve module 'metro-source-map'
warn Unable to resolve module 'nullthrows'
warn Unable to resolve module 'pretty-format'
warn Unable to resolve module 'promise'
warn Unable to resolve module 'react-devtools-core'
warn Unable to resolve module 'react-native-gradle-plugin'
warn Unable to resolve module 'react-refresh'
warn Unable to resolve module 'react-shallow-renderer'
warn Unable to resolve module 'regenerator-runtime'
warn Unable to resolve module 'scheduler'
warn Unable to resolve module 'stacktrace-parser'
warn Unable to resolve module 'use-subscription'
warn Unable to resolve module 'whatwg-fetch'
warn Unable to resolve module 'ws'
warn Unable to resolve module 'react-native-codegen'
```

# How I've managed to get it working

Setting `pnpm` to use hoisted mode:

in `<gitRoot>/.npmrc`:

```
module-linker=hoisted
```

Although hoisted mode doesn't require the symlink resolver to get metro functioning with pnpm
