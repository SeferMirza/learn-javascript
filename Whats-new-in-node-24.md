# Node 24

The following sources were consulted in preparing this document.

- https://blog.logrocket.com/node-js-24-new/
- https://nodejs.org/en/blog/release/v24.0.0
- ChatGPT

## URLPattern as a global

The `URLPattern` API is now exposed on the global object, making it easier to
use without explicit imports.

## Test Runner Enhancements

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

## `import.meta.main` is now available

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

## Upgrade to V24

Reviewing the official Node.js 24 release notes and using tools like node
`--trace-deprecation` during testing can help you spot and fix these issues
early.

To upgrade, you can use a version manager like nvm. You can install it pretty
easily with the code below:

```
nvm install 24
nvm use 24
```

That, or you can download the latest version directly from the Node.js website.