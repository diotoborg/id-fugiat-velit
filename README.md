# @diotoborg/id-fugiat-velit <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

An ESnext spec-compliant `Map.groupBy` shim/polyfill/replacement that works as far down as ES3.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the proposed [spec](https://tc39.github.io/proposal-array-grouping/).

## Getting started

```sh
npm install --save @diotoborg/id-fugiat-velit
```

## Usage/Examples

```js
var groupBy = require('@diotoborg/id-fugiat-velit');
var assert = require('assert');

var arr = [0, 1, 2, 3, 4, 5];
var parity = function (x) { return x % 2 === 0 ? 'even' : 'odd'; };

var results = groupBy(arr, function (x, i) {
    assert.equal(x, arr[i]);
    return parity(x);
});

assert.deepEqual(results, new Map([
    ['even', [0, 2, 4]],
    ['odd', [1, 3, 5]],
]));
```

```js
var groupBy = require('@diotoborg/id-fugiat-velit');
var assert = require('assert');
/* when Map.groupBy is not present */
delete Map.groupBy;
var shimmed = groupBy.shim();

assert.equal(shimmed, groupBy.getPolyfill());
assert.deepEqual(Map.groupBy(arr, parity), groupBy(arr, parity));
```

```js
var groupBy = require('@diotoborg/id-fugiat-velit');
var assert = require('assert');
/* when Array#group is present */
var shimmed = groupBy.shim();

assert.equal(shimmed, Map.groupBy);
assert.deepEqual(Map.groupBy(arr, parity), groupBy(arr, parity));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@diotoborg/id-fugiat-velit
[npm-version-svg]: https://versionbadg.es/diotoborg/id-fugiat-velit.svg
[deps-svg]: https://david-dm.org/diotoborg/id-fugiat-velit.svg
[deps-url]: https://david-dm.org/diotoborg/id-fugiat-velit
[dev-deps-svg]: https://david-dm.org/diotoborg/id-fugiat-velit/dev-status.svg
[dev-deps-url]: https://david-dm.org/diotoborg/id-fugiat-velit#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@diotoborg/id-fugiat-velit.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@diotoborg/id-fugiat-velit.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@diotoborg/id-fugiat-velit.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@diotoborg/id-fugiat-velit
[codecov-image]: https://codecov.io/gh/diotoborg/id-fugiat-velit/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/diotoborg/id-fugiat-velit/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/diotoborg/id-fugiat-velit
[actions-url]: https://github.com/diotoborg/id-fugiat-velit/actions
