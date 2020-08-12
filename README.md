
# morgan-body-ext

**Important Note:** The extra functionalities in this library have already been merge to it's parent [morgan-body](https://github.com/sirrodgepodge/morgan-body). Thanks!

##

This library is a customised version of the [morgan-body](https://github.com/sirrodgepodge/morgan-body).

The original [morgan-body](https://github.com/sirrodgepodge/morgan-body) lacks the functionality to log additional request/response tokens like 'Request ID' which would be useful for log tracing purposes.

[morgan-body-ext](https://github.com/jazzyinstyle/morgan-body-ext) additionally logs these tokens as part of the original log format:

* **id**: Request ID

* **request-headers**: Request headers (JSON string)

* **response-headers**: Response headers (JSON string)

You can also have the option to select only those request/response headers that you want to log by passing in these additional option-parameters:

* **logAllReqHeader**: *true* will log All request headers and take precedence over logReqHeaderList; *false* otherwise.
* **logReqHeaderList**: takes in a list of request headers to be displayed in the log.
* **logAllResHeader**: *true* will log All response headers and take precedence over logResHeaderList; *false* otherwise.
* **logResHeaderList**: takes in a list of response headers to be displayed in the log.
 
[![NPM][nodei-image]][nodei-url]


## Example of Use
```JS
const express = require('express');
const bodyParser = require('body-parser');
const morgan = require('morgan');
const morganBody = require('morgan-body-ext');

const app = express();

/* Using 'express-request-id' to generate UUID for request 
and add it to X-Request-Id header. 
In case request contains X-Request-Id header, it uses its value instead.
*/
const requestId = require('express-request-id')();

app.use(requestId);

/* Create the 'id' token in morgan that returns the Request ID. 
Refer https://www.npmjs.com/package/morgan#tokens for more details. 
*/
morgan.token('id', req => req.id); 

/* Parse body before morganBody as body will be logged */
app.use(bodyParser.json());

/* Hook morganBody to express app */
morganBody(app, {
  /* logAllReqHeader=true will log All request headers and take precedence over logReqHeaderList */
  logAllReqHeader: false,
  /* logReqHeaderList takes in a list of request headers to be displayed in the log */
  logReqHeaderList: ['host', 'content-length', 'cache-control', 'origin', 'content-type', 'accept'],
  /* logAllResHeader=true will log All response headers and take precedence over logResHeaderList */
  logAllResHeader: false,
  /* logResHeaderList takes in a list of response headers to be displayed in the log */
  logResHeaderList: ['host', 'content-length', 'cache-control', 'origin', 'content-type', 'accept']
});
```

## Example of Generated Logs
```
2018-09-19T02:32:57.526Z info: [4bc80c25-7748-4fc6-9592-772723333390] Request: POST /sample?test=123 headers[host=localhost:3000;content-length=321;cache-control=no-cache;origin=chrome-extension://aicmkgpgakddgnaphhhpliifpcfhicfo;content-type=application/json;accept=*/*;]
2018-09-19T02:32:57.527Z info: [4bc80c25-7748-4fc6-9592-772723333390] Request Body:{"detail":"123","detail2":{"some-id":"123"}}
2018-09-19T02:32:57.528Z info: [4bc80c25-7748-4fc6-9592-772723333390] Response Body:{"some response body"}
2018-09-19T02:32:57.530Z info: [4bc80c25-7748-4fc6-9592-772723333390] Response: 200 headers[-] 2923.631 ms - 27
```

## References
* Please refer to [morgan-body](https://github.com/sirrodgepodge/morgan-body) for more usage example.
* UUID generation for Request: [express-request-id](https://www.npmjs.com/package/express-request-id) 


[nodei-image]: https://nodei.co/npm/morgan-body-ext.png?downloads=true&downloadRank=true&stars=true
[nodei-url]: https://www.npmjs.com/package/morgan-body-ext
