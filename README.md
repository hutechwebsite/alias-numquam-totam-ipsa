# @hutechwebsite/alias-numquam-totam-ipsa <sup>[![Version Badge][npm-version-svg]][npm-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][npm-url]

An Object.assign shim. Invoke its "shim" method to shim Object.assign if it is unavailable.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the [spec](http://www.ecma-international.org/ecma-262/6.0/#sec-@hutechwebsite/alias-numquam-totam-ipsa). In an ES6 environment, it will also work properly with `Symbol`s.

Takes a minimum of 2 arguments: `target` and `source`.
Takes a variable sized list of source arguments - at least 1, as many as you want.
Throws a TypeError if the `target` argument is `null` or `undefined`.

Most common usage:
```js
var assign = require('@hutechwebsite/alias-numquam-totam-ipsa').getPolyfill(); // returns native method if compliant
	/* or */
var assign = require('@hutechwebsite/alias-numquam-totam-ipsa/polyfill')(); // returns native method if compliant
```

## Example

```js
var assert = require('assert');

// Multiple sources!
var target = { a: true };
var source1 = { b: true };
var source2 = { c: true };
var sourceN = { n: true };

var expected = {
	a: true,
	b: true,
	c: true,
	n: true
};

assign(target, source1, source2, sourceN);
assert.deepEqual(target, expected); // AWESOME!
```

```js
var target = {
	a: true,
	b: true,
	c: true
};
var source1 = {
	c: false,
	d: false
};
var sourceN = {
	e: false
};

var assigned = assign(target, source1, sourceN);
assert.equal(target, assigned); // returns the target object
assert.deepEqual(assigned, {
	a: true,
	b: true,
	c: false,
	d: false,
	e: false
});
```

```js
/* when Object.assign is not present */
delete Object.assign;
var shimmedAssign = require('@hutechwebsite/alias-numquam-totam-ipsa').shim();
	/* or */
var shimmedAssign = require('@hutechwebsite/alias-numquam-totam-ipsa/shim')();

assert.equal(shimmedAssign, assign);

var target = {
	a: true,
	b: true,
	c: true
};
var source = {
	c: false,
	d: false,
	e: false
};

var assigned = assign(target, source);
assert.deepEqual(Object.assign(target, source), assign(target, source));
```

```js
/* when Object.assign is present */
var shimmedAssign = require('@hutechwebsite/alias-numquam-totam-ipsa').shim();
assert.equal(shimmedAssign, Object.assign);

var target = {
	a: true,
	b: true,
	c: true
};
var source = {
	c: false,
	d: false,
	e: false
};

assert.deepEqual(Object.assign(target, source), assign(target, source));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[npm-url]: https://npmjs.org/package/@hutechwebsite/alias-numquam-totam-ipsa
[npm-version-svg]: http://versionbadg.es/ljharb/@hutechwebsite/alias-numquam-totam-ipsa.svg
[travis-svg]: https://travis-ci.org/ljharb/@hutechwebsite/alias-numquam-totam-ipsa.svg
[travis-url]: https://travis-ci.org/ljharb/@hutechwebsite/alias-numquam-totam-ipsa
[deps-svg]: https://david-dm.org/ljharb/@hutechwebsite/alias-numquam-totam-ipsa.svg?theme=shields.io
[deps-url]: https://david-dm.org/ljharb/@hutechwebsite/alias-numquam-totam-ipsa
[dev-deps-svg]: https://david-dm.org/ljharb/@hutechwebsite/alias-numquam-totam-ipsa/dev-status.svg?theme=shields.io
[dev-deps-url]: https://david-dm.org/ljharb/@hutechwebsite/alias-numquam-totam-ipsa#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@hutechwebsite/alias-numquam-totam-ipsa.png?downloads=true&stars=true
[license-image]: http://img.shields.io/npm/l/@hutechwebsite/alias-numquam-totam-ipsa.svg
[license-url]: LICENSE
[downloads-image]: http://img.shields.io/npm/dm/@hutechwebsite/alias-numquam-totam-ipsa.svg
[downloads-url]: http://npm-stat.com/charts.html?package=@hutechwebsite/alias-numquam-totam-ipsa
[codecov-image]: https://codecov.io/gh/ljharb/@hutechwebsite/alias-numquam-totam-ipsa/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@hutechwebsite/alias-numquam-totam-ipsa/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@hutechwebsite/alias-numquam-totam-ipsa
[actions-url]: https://github.com/hutechwebsite/alias-numquam-totam-ipsa/actions
