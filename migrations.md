# Migrations

It is the documentation of the migrations between versions, problems encountered
while migrating, solutions to problems and changes.

## Node 24

```markdown
- [ ] install or use `nvm install 24; nvm use 24` to use `24`th version
- update packages
  - [ ] `vue` 3.5.17 -> 3.5.21
  - [ ] `vite` 7.0.5 -> 7.1.5
  - [ ] `@nuxt/kit` 4.0.1 -> 4.1.1
  - [ ] `@primeuix/themes` 1.2.1 -> 1.2.3
  - [ ] `primevue` 4.3.6 -> 4.3.9
  - [ ] `@nuxt/devtools` 2.6.2 -> 2.6.3
  - [ ] `@nuxt/eslint-config` 1.7.0 -> 1.9.0
  - [ ] `@nuxt/module-builder` 1.0.1 -> 1.0.2
  - [ ] `@nuxt/schema` 4.0.1 -> 4.1.1
  - [ ] `@types/node` 24.0.15 -> 24.3.1
  - [ ] `eslint` 9.31.0 -> 9.35.0
  - [ ] `typescript` 5.8.3 -> 5.9.2
  - [ ] `vue-tsc` 3.0.3 -> 3.0.6
- [ ] use the '--trace-deprecation' flag during the run or build stage to list deprecations
  - deprecations;
    - [ ] remove asynchronous on testing
    - [ ] remove `URLPattern` imports
    - [ ] use `import.meta.main` to find the entry point
    - ...
  - warning;
    - if u on module
      - [ ] export types as `.d.mts`
      - [ ] export require as `.mjs`
      - ...
- [ ] update node version to 24 on workflows
```

The following sources were consulted in preparing this document.

- https://blog.logrocket.com/node-js-24-new/
- https://nodejs.org/en/blog/release/v24.0.0
- ChatGPT

### URLPattern as a global

The `URLPattern` API is now exposed on the global object, making it easier to
use without explicit imports.

### Test Runner Enhancements

The test runner module now automatically waits for subtests to finish,
eliminating the need to manually await test promises.

```javascript
import test from "node:test";

// old
test("parent test", (t) => {
  await t.test("subtest", async () => {
    console.log("running subtest");
  });
});

// new
test("parent test", (t) => {
  t.test("subtest", () => {
    console.log("running subtest");
  });
});
```

### `import.meta.main` is now available

Boolean value available in ECMAScript modules, which can be used to detect
whether the current module was the entry point of the current process.

```javascript
// module.js
export function foo() {
  return "Hello, world";
}

function main() {
  const message = foo();
  console.log(message);
}

// run if this module is the entry point
if (import.meta.main) main();

// main.js
import { foo } from "./module.js";

console.log(foo());
// main() function will not run because import.meta.main is false
```
