# Node 24

The following sources were consulted in preparing this document.

https://blog.logrocket.com/node-js-24-new/
https://nodejs.org/en/blog/release/v24.0.0
ChatGPT

## V8 engine is updated to version 13.6

- Float16Array -> new type
- Explicit resource management
  ```javascript
    import fs from "node:fs/promises";

    await using dir = await fs.opendir("./logs");

    for await (const dirent of dir) {
    console.log(dirent.name);
    }
    // No need to explicitly close the directory
  ```
- RegExp.escape
  ```javascript
    const pattern = RegExp.escape("file.*(txt|log)");
    console.log(pattern); // "file\.\*\(txt\|log\)"
    const re = new RegExp(pattern);
  ```
- WebAssembly Memory64 -> not for us
- Error.isError
  ```javascript
    console.log(Error.isError(new Error())); // true
    console.log(Error.isError({})); // false
  ```

## URLPattern as a global

The `URLPattern` API is now exposed on the global object, making it easier to
use without explicit imports.

## Test Runner Enhancements

The test runner module now automatically waits for subtests to finish,
eliminating the need to manually await test promises.

```javascript
import test from 'node:test';

// old
test('parent test', (t) => {
  await t.test('subtest', async () => {
    console.log('running subtest');
  });
});

// new
test('parent test', (t) => {
  t.test('subtest', () => {
    console.log('running subtest');
  });
});
```

## Watch

`--watch-kill-signal` flag added

## `import.meta.main` is now available

Boolean value available in ECMAScript modules, which can be used to detect
whether the current module was the entry point of the current process.

```javascript
// module.js
export function foo() {
  return 'Hello, world';
}

function main() {
  const message = foo();
  console.log(message);
}

// run if this module is the entry point
if (import.meta.main) main();

// x.js
import { foo } from './module.js';

console.log(foo());
// main() function will not run because import.meta.main is false
```

## Runtime deprecation of url.parse()

use the WHATWG URL API instead

```javascript
// Deprecated (throws runtime warning)
const parsed = require('url').parse('https://example.com');// alternative
const parsed = new URL('https://example.com');
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