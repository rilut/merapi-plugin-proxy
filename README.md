# merapi-plugin-proxy
Pluginable proxy for Merapi to enable it to do remote call other merapi services

## Installation
Install using npm:
```
npm install merapi-plugin-proxy --save
```

## Configuration

```
plugins:
    - proxy
components:
    proxyServiceNameV1: type: "proxy", uri: "http://localhost:5000", version: "v1",
    proxyServiceNameV2: type: "proxy", uri: "http://localhost:5000", version: "v2"
```

## Usage 
Manual
```
let proxyServiceV1 = await container.resolve("proxyServiceNameV1");
// call the proxy
let response = await proxyServiceV1.<functionName>(param1, param2);
```

Automatic injection
```
"use strict";
const {Component} = require("merapi");

module.exports = class FirstComponent extends Component {
    constructor(logger, proxyServiceNameV2) {
        super();
        this.proxyServiceV2 = proxyServiceNameV2;
        this.logger = logger;
    }
    *callProxy() {
        this.logger.info("execute proxy call");
        let res = yield this.proxyServiceV2.<functionName>(param1, param2);
        return res;
    }
};
```

## Copyright
Copyright (c) 2015-2016 YesBoss Group. All rights reserved.
We plan to open source this later in 2016, however please do not share
this before we officially release this as open source.

## Contributors
* Roni Kurniawan (Initial Contributor)
* Ikmal Syifai
* Ahmad Rizqi Meydiarso