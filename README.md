bunyan-request-logger
=====================

[![Join the chat at https://gitter.im/nixplay/bunyan-request-logger](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/nixplay/bunyan-request-logger?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Automated request logging connect middleware for Express. Powered by Bunyan.


Example usage:

```
$ npm install --save bunyan-request-logger
```

```js
'use strict';

var express = require('express'),
  logger = require('../request-logger.js'),
  noCache = require('connect-cache-control'),
  log = logger(),
  app = express(),
  port = 3000;

app.use( log.requestLogger() );

// Route to handle client side log messages.
//
// This route prepends the cache-control
// middleware so that the browser always logs
// to the server instead of fetching a useless
// OK message from its cache.
// 
// Using a 1x1 transparent gif allows you to
// use the logger in emails or embed the tracking
// pixel on third party sites without resorting
// to JavaScript.
app.get( '/log.gif', noCache, log.route() );

app.listen(port, function () {
  log.info('Listening on port ' + port);
});
```
