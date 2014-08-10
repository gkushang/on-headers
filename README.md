# on-headers [![Build Status](https://travis-ci.org/expressjs/on-headers.svg)](https://travis-ci.org/expressjs/on-headers) [![NPM version](https://badge.fury.io/js/on-headers.svg)](http://badge.fury.io/js/on-headers)

Execute a listener when a response is about to write headers.

## Install

```sh
$ npm install on-headers
```

## API

```js
var onHeaders = require('on-headers')
```

### onHeaders(res, listener)

This will add the listener `listener` to fire when headers are emitted for `res`.
Headers are considered to be emitted only once, right before they are sent to
the client.

## Examples

```js
var http = require('http')
var onHeaders = require('on-headers')

http
.createServer(onRequest)
.listen(3000)

function addPoweredBy() {
  // add if not set by end of request
  if (!this.getHeader('X-Powered-By')) {
    this.addHeader('X-Powered-By', 'Node.js')
  }
}

function onRequest(req, res) {
  onHeaders(res, addPoweredBy)

  res.setHeader('Content-Type', 'text/plain')
  res.end('hello!')
}
```

## License

[MIT](LICENSE)
