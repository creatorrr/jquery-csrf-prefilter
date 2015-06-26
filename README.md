# jquery-csrf-prefilter

[jQuery prefilter][jquery-ajaxprefilter] for automatically inserting a CSRF
token with every destructive AJAX request.

[![npm Version][npm-badge]][npm]
[![Build Status][build-badge]][build-status]
[![Test Coverage][coverage-badge]][coverage-result]
[![Dependency Status][dep-badge]][dep-status]

## Installation

Install using npm:

    $ npm install jquery-csrf-prefilter

## Usage

__jquery-csrf-prefilter__ is a factory function that, given a CSRF token
string, will return a function that can be passed to `$.ajaxPrefilter` to
inject the token into subsequent AJAX requests. By default, this prefilter will
add the token via a `X-CSRF-Token` header with all requests that are not of the
types GET, OPTIONS, HEAD, or TRACE. This functionality can be further
customized with a second `options` param.

Basic example which adds a `X-CSRF-Token` header with each POST, PUT, PATCH,
and DELETE request:

```js
var $ = require('jquery'),
    createCsrfPrefilter = require('jquery-csrf-token'),
    tokenValue = $('meta[name="csrf-token"]').attr('content');

$.ajaxPrefilter(createCsrfPrefilter(tokenValue));
```

## Available Options

The following options may be specified when creating a CSRF prefilter:

### `header` (string)

Specify the header that is to be used. Replaces the default `X-CSRF-Token`
header.  This option may be specified in addition to `data` and/or `query`; all
will be added to the request.

Example:

```js
$.ajaxPrefilter(createCsrfPrefilter(tokenValue, { header: 'X-CSRFToken' }));`
```

### `data` (string)

Key that is to be added to the form/JSON data payload of the request. Replaces
the default `X-CSRF-Token` header.  This option may be specified in addition to
`header` and/or `query`; all will be added to the request.

Example:

```js
$.ajaxPrefilter(createCsrfPrefilter(tokenValue, { data: '_csrf' }));`
```

### `query` (string)

Key that is to be added as a query param to the request. Replaces the default
`X-CSRF-Token` header.  This option may be specified in addition to `header`
and/or `data`; all will be added to the request.

Example:

```js
$.ajaxPrefilter(createCsrfPrefilter(tokenValue, { query: '_csrf' }));`
```

### `ignoreMethods` (array)

Request methods to be ignored for the purposes of injecting the CSRF token. By
default, this value is `['GET', 'OPTIONS', 'HEAD', 'TRACE']`.

## License

MIT

[build-badge]: https://img.shields.io/travis/jimf/jquery-csrf-prefilter/master.svg
[build-status]: https://travis-ci.org/jimf/jquery-csrf-prefilter
[npm-badge]: https://img.shields.io/npm/v/jquery-csrf-prefilter.svg
[npm]: https://www.npmjs.org/package/jquery-csrf-prefilter
[coverage-badge]: https://img.shields.io/coveralls/jimf/jquery-csrf-prefilter.svg
[coverage-result]: https://coveralls.io/r/jimf/jquery-csrf-prefilter
[dep-badge]: https://img.shields.io/david/jimf/jquery-csrf-prefilter.svg
[dep-status]: https://david-dm.org/jimf/jquery-csrf-prefilter
[jquery-ajaxprefilter]: http://api.jquery.com/jquery.ajaxprefilter/
