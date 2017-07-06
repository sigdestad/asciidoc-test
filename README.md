Http Client Library for Enonic XP
=================================

[![Build Status](https://travis-ci.org/enonic/lib-http-client.svg?branch=master)](https://travis-ci.org/enonic/lib-http-client)
[![codecov](https://codecov.io/gh/enonic/lib-http-client/branch/master/graph/badge.svg)](https://codecov.io/gh/enonic/lib-http-client)
[![License](https://img.shields.io/github/license/enonic/lib-http-client.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)

This library allows making HTTP requests to a remote server and receiving the response.
See documentation here: https://enonic-docs.s3.amazonaws.com/com.enonic.lib/lib-http-client/index.html


## Building

To build this project, execute the following:

```
./gradlew clean build
```

## Publishing

To release this project, execute the following:

```
./gradlew clean build uploadArchives
```

## Documentation

Building the documentation is done executing the following:

```
./gradlew buildDoc
```

And publishing the docs to S3:

```
./gradlew publishDoc
```
