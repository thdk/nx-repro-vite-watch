# Repro for issue with @nx/vite

Watch mode doesn't work for projects using `@nx/vite`.

For other bundlers like `@nx/webpack` watch mode does still work.

## Steps to reproduce

```sh
# npx nx g @nx/react:app my-app --bundler=vite
npx nx test my-app --watch
```

Expected:

Should run the tests and then wait for changes.
When changes are made, tests should rerun.

Actual:

```sh
> nx run my-app:test --watch

The CJS build of Vite's Node API is deprecated. See https://vitejs.dev/guide/troubleshooting.html#vite-cjs-node-api-deprecated for more details.
 Vitest  "cache.dir" is deprecated, use Vite's "cacheDir" instead if you want to change the cache director. Note caches will be written to "cacheDir/vitest"

 RUN  v1.4.0 /Users/thdk/repos/thdk/nx/nx-react-vite/my-app

stderr | src/app/app.spec.tsx > App > should have a greeting as the title
To match all elements we had to reset the lastIndex of the RegExp because the global flag is enabled. We encourage to remove the global flag from the RegExp.

 ✓ src/app/app.spec.tsx (2)
   ✓ App (2)
     ✓ should render successfully
     ✓ should have a greeting as the title

 Test Files  1 passed (1)
      Tests  2 passed (2)
   Start at  13:32:54
   Duration  724ms (transform 65ms, setup 0ms, collect 193ms, tests 72ms, environment 286ms, prepare 50ms)


——————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 NX   Successfully ran target test for project my-app
```

This workspace also contains a react app that is configured with webpack.
For this project watch mode still works.

```sh
# npx nx g @nx/react:app webpack-app --bundler=webpack
npx nx test webpack-app --watch
```

## NX report

```sh

❯ npx nx report

 NX   Report complete - copy this into the issue template

Node   : 20.10.0
OS     : darwin-arm64
npm    : 10.2.3

nx                 : 18.1.1
@nx/js             : 18.1.1
@nx/jest           : 18.1.1
@nx/linter         : 18.1.1
@nx/eslint         : 18.1.1
@nx/workspace      : 18.1.1
@nx/devkit         : 18.1.1
@nx/eslint-plugin  : 18.1.1
@nx/react          : 18.1.1
@nrwl/tao          : 18.1.1
@nx/vite           : 18.1.1
@nx/web            : 18.1.1
@nx/webpack        : 18.1.1
typescript         : 5.3.3
```
