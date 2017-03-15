# find-callsite [![NPM version](https://img.shields.io/npm/v/find-callsite.svg?style=flat)](https://www.npmjs.com/package/find-callsite) [![mit license][license-img]][license-url] [![NPM monthly downloads](https://img.shields.io/npm/dm/find-callsite.svg?style=flat)](https://npmjs.org/package/find-callsite) [![npm total downloads][downloads-img]][downloads-url]

> Finds the correct place where the stack trace was started, not the place where error was thrown

[![code climate][codeclimate-img]][codeclimate-url] 
[![code style][standard-img]][standard-url] 
[![linux build][travis-img]][travis-url] 
[![windows build][appveyor-img]][appveyor-url] 
[![code coverage][coverage-img]][coverage-url] 
[![dependency status][david-img]][david-url]
[![paypal donate][paypalme-img]][paypalme-url] 

You might also be interested in [stacktrace-metadata](https://github.com/tunnckocore/stacktrace-metadata#readme).

## Table of Contents
- [Install](#install)
- [Usage](#usage)
- [API](#api)
  * [findCallsite](#findcallsite)
- [Related](#related)
- [Contributing](#contributing)
- [Building docs](#building-docs)
- [Running tests](#running-tests)
- [Author](#author)
- [License](#license)

## Install
Install with [npm](https://www.npmjs.com/)

```
$ npm install find-callsite --save
```

or install using [yarn](https://yarnpkg.com)

```
$ yarn add find-callsite
```

## Usage
> For more use-cases see the [tests](test.js)

```js
const findCallsite = require('find-callsite')
```

## API

### [findCallsite](index.js#L55)
> Find correct callsite where error is started. All that stuff is because you not always need the first line of the stack to understand where and what happened.

In below example we use `rimraf.sync` to throw some error. That's
the case when we need to be informed where is the `rimraf.sync` call
not where it throws. In that case it is on line 6, column 12.

**Params**

* `error` **{Error|Object|String}**: plain or Error object with stack property, or string stack    
* `opts` **{Object}**: optional options object    
* `opts.cwd` **{String}**: give current working directory, default to `process.cwd()`    
* `opts.relativePaths` **{Boolean}**: make path relative to `opts.cwd`, default `false`    
* `returns` **{String}**: single callsite from whole stack trace, e.g. `at foo (/home/bar/baz.js:33:4)`  

**Example**

```js
var findCallsite = require('find-callsite')
var rimraf = require('rimraf')

function fixture () {
  try {
    rimraf.sync(5555)
  } catch (err) {
    var callsiteLine = findCallsite(err)
    console.log(callsiteLine)
    // => 'at fixture (/home/charlike/apps/find-callsite/example.js:6:12)'

    var relativeCallsiteLine = findCallsite(err, {
      relativePaths: true
    })
    console.log(relativeCallsiteLine)
    // => 'at fixture (example.js:6:12)'
  }
}

fixture()
```

## Related
- [always-done](https://www.npmjs.com/package/always-done): Handle completion and errors with elegance! Support for streams, callbacks, promises, child processes, async/await and sync functions. A drop-in replacement… [more](https://github.com/hybridables/always-done#readme) | [homepage](https://github.com/hybridables/always-done#readme "Handle completion and errors with elegance! Support for streams, callbacks, promises, child processes, async/await and sync functions. A drop-in replacement for [async-done][] - pass 100% of its tests plus more")
- [assert-kindof](https://www.npmjs.com/package/assert-kindof): Check native type of value and throw AssertionError if not okey. Clean stack traces. Simplicity. Built on [is-kindof][]. | [homepage](https://github.com/tunnckocore/assert-kindof#readme "Check native type of value and throw AssertionError if not okey. Clean stack traces. Simplicity. Built on [is-kindof][].")
- [clean-stacktrace-metadata](https://www.npmjs.com/package/clean-stacktrace-metadata): Plugin for `clean-stacktrace` lib. Parse each line to get additional info like `filename`, `column` and `line` of the error. | [homepage](https://github.com/tunnckocore/clean-stacktrace-metadata#readme "Plugin for `clean-stacktrace` lib. Parse each line to get additional info like `filename`, `column` and `line` of the error.")
- [clean-stacktrace-relative-paths](https://www.npmjs.com/package/clean-stacktrace-relative-paths): Meant to be used with [clean-stacktrace][] as mapper function. Makes absolute paths inside stack traces to relative paths. | [homepage](https://github.com/tunnckocore/clean-stacktrace-relative-paths#readme "Meant to be used with [clean-stacktrace][] as mapper function. Makes absolute paths inside stack traces to relative paths.")
- [clean-stacktrace](https://www.npmjs.com/package/clean-stacktrace): Clean up error stack traces from node internals | [homepage](https://github.com/tunnckocore/clean-stacktrace#readme "Clean up error stack traces from node internals")
- [error-format](https://www.npmjs.com/package/error-format): Allows you to customize the toString method of passed `err`. Also adds useful properties like `line`, `filename` and `column` to… [more](https://github.com/tunnckocore/error-format#readme) | [homepage](https://github.com/tunnckocore/error-format#readme "Allows you to customize the toString method of passed `err`. Also adds useful properties like `line`, `filename` and `column` to the `err` object.")
- [is-async-function](https://www.npmjs.com/package/is-async-function): Is function really asynchronous function? Trying to guess that based on check if [common-callback-names][] exists as function arguments names or… [more](https://github.com/tunnckocore/is-async-function#readme) | [homepage](https://github.com/tunnckocore/is-async-function#readme "Is function really asynchronous function? Trying to guess that based on check if [common-callback-names][] exists as function arguments names or you can pass your custom.")
- [minibase](https://www.npmjs.com/package/minibase): Minimalist alternative for Base. Build complex APIs with small units called plugins. Works well with most of the already existing… [more](https://github.com/node-minibase/minibase#readme) | [homepage](https://github.com/node-minibase/minibase#readme "Minimalist alternative for Base. Build complex APIs with small units called plugins. Works well with most of the already existing [base][] plugins.")
- [parse-function](https://www.npmjs.com/package/parse-function): Parse a function into an object that has its name, body, args and a few more useful properties. | [homepage](https://github.com/tunnckocore/parse-function#readme "Parse a function into an object that has its name, body, args and a few more useful properties.")
- [stacktrace-metadata](https://www.npmjs.com/package/stacktrace-metadata): Modify given `err` object to be more useful - adds `line`, `column` and `filename` properties and also cleans stack traces. | [homepage](https://github.com/tunnckocore/stacktrace-metadata#readme "Modify given `err` object to be more useful - adds `line`, `column` and `filename` properties and also cleans stack traces.")
- [try-catch-core](https://www.npmjs.com/package/try-catch-core): Low-level package to handle completion and errors of sync or asynchronous functions, using [once][] and [dezalgo][] libs. Useful for and… [more](https://github.com/hybridables/try-catch-core#readme) | [homepage](https://github.com/hybridables/try-catch-core#readme "Low-level package to handle completion and errors of sync or asynchronous functions, using [once][] and [dezalgo][] libs. Useful for and used in higher-level libs such as [always-done][] to handle completion of anything.")

## Contributing
Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/tunnckoCore/find-callsite/issues/new).  
Please read the [contributing guidelines](CONTRIBUTING.md) for advice on opening issues, pull requests, and coding standards.  
If you need some help and can spent some cash, feel free to [contact me at CodeMentor.io](https://www.codementor.io/tunnckocore?utm_source=github&utm_medium=button&utm_term=tunnckocore&utm_campaign=github) too.

**In short:** If you want to contribute to that project, please follow these things

1. Please DO NOT edit [README.md](README.md), [CHANGELOG.md](CHANGELOG.md) and [.verb.md](.verb.md) files. See ["Building docs"](#building-docs) section.
2. Ensure anything is okey by installing the dependencies and run the tests. See ["Running tests"](#running-tests) section.
3. Always use `npm run commit` to commit changes instead of `git commit`, because it is interactive and user-friendly. It uses [commitizen][] behind the scenes, which follows Conventional Changelog idealogy.
4. Do NOT bump the version in package.json. For that we use `npm run release`, which is [standard-version][] and follows Conventional Changelog idealogy.

Thanks a lot! :)

## Building docs
Documentation and that readme is generated using [verb-generate-readme][], which is a [verb][] generator, so you need to install both of them and then run `verb` command like that

```
$ npm install verbose/verb#dev verb-generate-readme --global && verb
```

_Please don't edit the README directly. Any changes to the readme must be made in [.verb.md](.verb.md)._

## Running tests
Clone repository and run the following in that cloned directory

```
$ npm install && npm test
```

## Author
**Charlike Mike Reagent**

+ [github/tunnckoCore](https://github.com/tunnckoCore)
+ [twitter/tunnckoCore](https://twitter.com/tunnckoCore)
+ [codementor/tunnckoCore](https://codementor.io/tunnckoCore)

## License
Copyright © 2017, [Charlike Mike Reagent](https://i.am.charlike.online). Released under the [MIT License](LICENSE).

***

_This file was generated by [verb-generate-readme](https://github.com/verbose/verb-generate-readme), v0.4.3, on March 15, 2017._  
_Project scaffolded using [charlike][] cli._

[always-done]: https://github.com/hybridables/always-done
[async-done]: https://github.com/gulpjs/async-done
[base]: https://github.com/node-base/base
[charlike]: https://github.com/tunnckocore/charlike
[clean-stacktrace]: https://github.com/tunnckocore/clean-stacktrace
[commitizen]: https://github.com/commitizen/cz-cli
[common-callback-names]: https://github.com/tunnckocore/common-callback-names
[dezalgo]: https://github.com/npm/dezalgo
[is-kindof]: https://github.com/tunnckocore/is-kindof
[once]: https://github.com/isaacs/once
[standard-version]: https://github.com/conventional-changelog/standard-version
[verb-generate-readme]: https://github.com/verbose/verb-generate-readme
[verb]: https://github.com/verbose/verb

[license-url]: https://www.npmjs.com/package/find-callsite
[license-img]: https://img.shields.io/npm/l/find-callsite.svg

[downloads-url]: https://www.npmjs.com/package/find-callsite
[downloads-img]: https://img.shields.io/npm/dt/find-callsite.svg

[codeclimate-url]: https://codeclimate.com/github/tunnckoCore/find-callsite
[codeclimate-img]: https://img.shields.io/codeclimate/github/tunnckoCore/find-callsite.svg

[travis-url]: https://travis-ci.org/tunnckoCore/find-callsite
[travis-img]: https://img.shields.io/travis/tunnckoCore/find-callsite/master.svg?label=linux

[appveyor-url]: https://ci.appveyor.com/project/tunnckoCore/find-callsite
[appveyor-img]: https://img.shields.io/appveyor/ci/tunnckoCore/find-callsite/master.svg?label=windows

[coverage-url]: https://codecov.io/gh/tunnckoCore/find-callsite
[coverage-img]: https://img.shields.io/codecov/c/github/tunnckoCore/find-callsite/master.svg

[david-url]: https://david-dm.org/tunnckoCore/find-callsite
[david-img]: https://img.shields.io/david/tunnckoCore/find-callsite.svg

[standard-url]: https://github.com/feross/standard
[standard-img]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg

[paypalme-url]: https://www.paypal.me/tunnckoCore
[paypalme-img]: https://img.shields.io/badge/paypal-donate-brightgreen.svg

