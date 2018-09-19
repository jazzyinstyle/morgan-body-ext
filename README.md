# morgan-body-ext

This library is a customised version of the [morgan-body](https://github.com/sirrodgepodge/morgan-body).

The original [morgan-body](https://github.com/sirrodgepodge/morgan-body) lacks the functionality to log additional request/response tokens like 'Request ID' which would useful for log tracing purposes.

[morgan-body-ext](https://github.com/jazzyinstyle/morgan-body-ext) additionally logs these tokens as part of the original log format:

**id**: Request ID

**request-headers**: Request headers (JSON string)

**response-headers**: Response headers (JSON string)


[![NPM][nodei-image]][nodei-url]

## Example of Generated Logs
```
2018-09-19T02:32:57.526Z info: [4bc80c25-7748-4fc6-9592-772723333390] Request: POST /sample?test=123 headers[{"host":"somehost:4000","connection":"keep-alive","content-length":"457","user-agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36","cache-control":"no-cache","origin":"some-origin","param1":"8888","content-type":"application/json","accept":"*/*","accept-encoding":"gzip, deflate, br","accept-language":"en-US,en;q=0.9","cookie":"some-cookie"}]
2018-09-19T02:32:57.527Z info: Request Body:{"detail":"123","detail2":{"some-id":"123"}}
2018-09-19T02:32:57.528Z info: Response Body:{"some response body"}
2018-09-19T02:32:57.530Z info: [4bc80c25-7748-4fc6-9592-772723333390] Response: 200 headers[-] 2923.631 ms - 27
```

Please refer to [morgan-body](https://github.com/sirrodgepodge/morgan-body) for usage example.

[nodei-image]: https://nodei.co/npm/morgan-body-ext.png?downloads=true&downloadRank=true&stars=true
[nodei-url]: https://www.npmjs.com/package/morgan-body-ext
