Http Client Library for Enonic XP
=================================

[![Build Status](https://travis-ci.org/enonic/lib-http-client.svg?branch=master)](https://travis-ci.org/enonic/lib-http-client)
[![codecov](https://codecov.io/gh/enonic/lib-http-client/branch/master/graph/badge.svg)](https://codecov.io/gh/enonic/lib-http-client)
[![License](https://img.shields.io/github/license/enonic/lib-http-client.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)


## Documentation

### Usage

Add Enonic repository to the repository list in the build.gradle file:

    repositories {
        maven {
            url 'http://repo.enonic.com/public'
        }
    }

After this, add the following dependency:

    dependencies {
        include 'com.enonic.lib:lib-http-client:1.0.0'
    }


### function request(params)
Sends an HTTP request and returns the response received from the remote server.
The request is sent synchronously, the execution blocks until the response is received.


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| params | <code>object</code> |  | JSON parameters. |
| params.url | <code>string</code> |  | URL to which the request is sent. |
| [params.method] | <code>string</code> | <code>&quot;GET&quot;</code> | The HTTP method to use for the request (e.g. "POST", "GET", "HEAD", "PUT", "DELETE"). |
| [params.params] | <code>object</code> |  | Query or form parameters to be sent with the request. |
| [params.headers] | <code>object</code> |  | HTTP headers, an object where the keys are header names and the values the header values. |
| [params.connectionTimeout] | <code>number</code> | <code>10000</code> | The timeout on establishing the connection, in milliseconds. |
| [params.readTimeout] | <code>number</code> | <code>10000</code> | The timeout on waiting to receive data, in milliseconds. |
| [params.body] | <code>string</code> \| <code>\*</code> |  | Body content to send with the request, usually for POST or PUT requests. It can be of type string or stream. |
| [params.contentType] | <code>string</code> |  | Content type of the request. |
| [params.multipart] | <code>Array.&lt;object&gt;</code> |  | Multipart form data to send with the request, an array of part objects. Each part object contains 'name', 'value', and optionally 'fileName' and 'contentType' properties. Where 'value' can be either a string or a Stream object. |
| [params.auth] | <code>object</code> |  | Settings for basic authentication. |
| [params.auth.user] | <code>string</code> |  | User name for basic authentication. |
| [params.auth.password] | <code>string</code> |  | Password for basic authentication. |
| [params.proxy] | <code>object</code> |  | Proxy settings. |
| [params.proxy.host] | <code>string</code> |  | Proxy host name to use. |
| [params.proxy.port] | <code>number</code> |  | Proxy port to use. |
| [params.proxy.user] | <code>string</code> |  | User name for proxy authentication. |
| [params.proxy.password] | <code>string</code> |  | Password for proxy authentication. |


#### Response : <code>Object</code>

| Name | Type | Description |
| --- | --- | --- |
| status | <code>number</code> | HTTP status code returned. |
| message | <code>string</code> | HTTP status message returned. |
| headers | <code>object</code> | HTTP headers of the response. |
| contentType | <code>string</code> | Content type of the response. |
| body | <code>string</code> | Body of the response as string. Null if the response content-type is not of type text. |
| bodyStream | <code>\*</code> | Body of the response as a stream object. |


### Examples:


**HTTP POST request**  
```js
var httpClientLib = require('/lib/http-client');

var response = httpClientLib.request({
    url: 'http://somehost/my/service',
    method: 'POST',
    headers: {
        'X-Custom-Header': 'header-value'
    },
    connectionTimeout: 20000,
    readTimeout: 5000,
    body: '{"id": 123}',
    contentType: 'application/json'
});

var expectedResponse = {
    'status': 200,
    'message': 'OK',
    'body': 'POST request',
    'contentType': 'text/plain',
    'headers': {
        'Content-Length': '12',
        'content-type': 'text/plain'
    }
};
```


**HTTP request with Basic Authentication**  
```js
var httpClientLib = require('/lib/http-client');

var response = httpClientLib.request({
    url: 'http://somehost/protected/service',
    method: 'GET',
    auth: {
        user: 'username',
        password: 'secret'
    }
});
```


**HTTP request via Proxy**  
```js
var httpClientLib = require('/lib/http-client');

var response = httpClientLib.request({
    url: 'http://somehost/some/service',
    method: 'GET',
    proxy: {
        host: '172.16.0.42',
        port: 8080,
        user: 'admin',
        password: 'secret'
    }
});
```


**Multipart POST request**  
```js
var httpClientLib = require('/lib/http-client');

var response = httpClientLib.request({
    url: 'http://somehost/uploadMedia',
    method: 'POST',
    contentType: 'multipart/mixed',
    multipart: [
        {
            name: 'media',
            fileName: 'logo.png',
            contentType: 'image/png',
            value: myImageStream
        },
        {
            name: 'category',
            value: 'images'
        }
    ]
});
```