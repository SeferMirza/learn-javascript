# Node 24

## V8 engine is updated to version 13.6

- Float16Array
- Explicit resource management
- RegExp.escape
- WebAssembly Memory64
- Error.isError

## npm 11

Node.js 24 comes with npm 11

## AsyncLocalStorage defaults to AsyncContextFrame

`AsyncLocalStorage` now uses `AsyncContextFrame` by default, which provides a
more efficient implementation of asynchronous context tracking.

## URLPattern as a global

The `URLPattern` API is now exposed on the global object, making it easier to
use without explicit imports.

## Permission Model Improvements

The experimental Permission Model introduced in Node.js 20 has been improved,
and the flag has been changed from `--experimental-permission` to simply
`--permission`, indicating its increasing stability and readiness for broader
adoption.

## Test Runner Enhancements

The test runner module now automatically waits for subtests to finish,
eliminating the need to manually await test promises.

## Undici 7

Node.js 24 includes Undici 7, which brings numerous improvements to the HTTP
client capabilities, including better performance and support for newer HTTP
features.

## Deprecations and Removals

Several APIs have been deprecated or removed in this release:

- Runtime deprecation of url.parse() - use the WHATWG URL API instead
- Removal of deprecated tls.createSecurePair
- Runtime deprecation of SlowBuffer
- Runtime deprecation of instantiating REPL without new
- Deprecation of using Zlib classes without new
- Deprecation of passing args to spawn and execFile in child_process

## Stability & modernization

### Deprecated/removed legacy APIs

There are a few legacy APIs deprecated or removed in this release.

### URL parsing

`url.parse()` is deprecated. It is recommended that the WHATWG URL API to be
used as it is more standards-compliant and secure.

```javascript
// Deprecated (throws runtime warning)
const parsed = require('url').parse('https://example.com');// alternative
const parsed = new URL('https://example.com');
```

### TLS security upgrade

The deprecated tls.createSecurePair is removed.

```javascript
// Removed (no longer available)
require('tls').createSecurePair();

// Use TLSSocket instead
new tls.TLSSocket(socket, options);
```

### Deprecation of SlowBuffer

SlowBuffer is deprecated now. If it is used, a runtime warning will be thrown.

```javascript
// Deprecated (use Buffer.allocUnsafeSlow)
const slow = new SlowBuffer(10);

// Modern alternative
const slow = Buffer.allocUnsafeSlow(10);
```

### Mandatory new keyword for REPL/Zlib classes

It is now runtime-deprecated to create a REPL instance or use Zlib classes
without the new keyword. This change aims to better align with standard
JavaScript class conventions.

## Upgrade to V24

As you plan your upgrade, keep in mind that some APIs and patterns have been
deprecated. These changes may require updates to legacy code, especially if your
project uses features like REPL or Zlib without the new keyword, or passes
arguments incorrectly to child_process methods. Reviewing the official Node.js
24 release notes and using tools like node --trace-deprecation during testing
can help you spot and fix these issues early.

To upgrade, you can use a version manager like nvm. You can install it pretty
easily with the code below:

```
nvm install 24
nvm use 24
```

That, or you can download the latest version directly from the Node.js website.

Since Node.js 24 will enter LTS in October 2025, now’s the time to explore its
new features. Whether you’re maintaining node apps or building new projects,
getting ahead of the curve will help keep your stack secure, stable, and
future-ready.