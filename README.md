# @firanorg/delectus-eligendi-quae <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

ES 2021 spec-compliant shim for Promise.any. Invoke its "shim" method to shim `Promise.any` if it is unavailable or noncompliant. **Note**: a global `Promise` must already exist: the [es6-shim](https://github.com/es-shims/es6-shim) is recommended.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment that has `Promise` available globally, and complies with the [spec](https://tc39.es/ecma262/#sec-@firanorg/delectus-eligendi-quae).

Most common usage:
```js
var assert = require('assert');
var any = require('@firanorg/delectus-eligendi-quae');

var resolved = Promise.resolve(42);
var rejected = Promise.reject(-1);
var alsoRejected = Promise.reject(Infinity);

any([resolved, rejected, alsoRejected]).then(function (result) {
	assert.equal(result, 42);
});

any([rejected, alsoRejected]).catch(function (error) {
	assert.ok(error instanceof AggregateError);
	assert.deepEqual(error.errors, [-1, Infinity]);
});

any.shim(); // will be a no-op if not needed

Promise.any([resolved, rejected, alsoRejected]).then(function (result) {
	assert.equal(result, 42);
});

Promise.any([rejected, alsoRejected]).catch(function (error) {
	assert.ok(error instanceof AggregateError);
	assert.deepEqual(error.errors, [-1, Infinity]);
});
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

## Pre-1.0 versions

The `@firanorg/delectus-eligendi-quae` package was released as now-deprecated v0.1.0 and v0.1.1, as a fork of https://github.com/m0ppers/promise-any.

Thanks to @sadorlovsky for donating the repo and the `@firanorg/delectus-eligendi-quae` npm package!

[package-url]: https://npmjs.com/package/@firanorg/delectus-eligendi-quae
[npm-version-svg]: https://versionbadg.es/firanorg/delectus-eligendi-quae.svg
[deps-svg]: https://david-dm.org/firanorg/delectus-eligendi-quae.svg
[deps-url]: https://david-dm.org/firanorg/delectus-eligendi-quae
[dev-deps-svg]: https://david-dm.org/firanorg/delectus-eligendi-quae/dev-status.svg
[dev-deps-url]: https://david-dm.org/firanorg/delectus-eligendi-quae#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@firanorg/delectus-eligendi-quae.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@firanorg/delectus-eligendi-quae.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@firanorg/delectus-eligendi-quae.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@firanorg/delectus-eligendi-quae
[codecov-image]: https://codecov.io/gh/firanorg/delectus-eligendi-quae/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/firanorg/delectus-eligendi-quae/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/firanorg/delectus-eligendi-quae
[actions-url]: https://github.com/firanorg/delectus-eligendi-quae/actions
