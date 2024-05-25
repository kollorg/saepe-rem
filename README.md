# @kollorg/saepe-rem <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

`Array.prototype.concat`, but made safe by ignoring Symbol.isConcatSpreadable

## Getting started

```sh
npm install --save @kollorg/saepe-rem
```

## Usage/Examples

```js
var safeConcat = require('@kollorg/saepe-rem');
var assert = require('assert');

assert.deepEqual([].concat([1, 2], 3, [[4]]), [1, 2, 3, [4]], 'arrays spread as expected with normal concat');
assert.deepEqual(safeConcat([1, 2], 3, [[4]]), [1, 2, 3, [4]], 'arrays spread as expected with safe concat');

String.prototype[Symbol.isConcatSpreadable] = true;
assert.deepEqual([].concat('foo', Object('bar')), ['foo', 'b', 'a', 'r'], 'spreadable String objects are spread with normal concat!!!');
assert.deepEqual(safeConcat('foo', Object('bar')), ['foo', Object('bar')], 'spreadable String objects are not spread with safe concat');

Array.prototype[Symbol.isConcatSpreadable] = false;
assert.deepEqual([].concat([1, 2], 3, [[4]]), [[], [1, 2], 3, [[4]]], 'non-concat-spreadable arrays do not spread with normal concat!!!');
assert.deepEqual(safeConcat([1, 2], 3, [[4]]), [1, 2, 3, [4]], 'non-concat-spreadable arrays still spread with safe concat');
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@kollorg/saepe-rem
[npm-version-svg]: https://versionbadg.es/ljharb/@kollorg/saepe-rem.svg
[deps-svg]: https://david-dm.org/ljharb/@kollorg/saepe-rem.svg
[deps-url]: https://david-dm.org/ljharb/@kollorg/saepe-rem
[dev-deps-svg]: https://david-dm.org/ljharb/@kollorg/saepe-rem/dev-status.svg
[dev-deps-url]: https://david-dm.org/ljharb/@kollorg/saepe-rem#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@kollorg/saepe-rem.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@kollorg/saepe-rem.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@kollorg/saepe-rem.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@kollorg/saepe-rem
[codecov-image]: https://codecov.io/gh/ljharb/@kollorg/saepe-rem/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@kollorg/saepe-rem/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@kollorg/saepe-rem
[actions-url]: https://github.com/kollorg/saepe-rem/actions
