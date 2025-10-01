---
layout: post
title: "Using Axios To Manage API"
date: 2025-08-19 10:24:00
category: program
tags: [react, axios]
---

```xml
├── src   
│   └── apis   
│       ├── configs   
│       │  ├── axiosConfigs.js  
│       │  └── axiosUtils.js  
│       ├── codeAPI.js
│       └── loginAPI.js

```

### axiosConfigs.js
```javascript
import axios from "axios";

export const api = axios.create({
    baseURL: process.env.PUBLIC_URL
});

// defining a custom error handler for all APIs
const errorHandler = (error) => {
    if (error.code === "ERR_CANCELED") {
        return Promise.resolve()
    }

    return Promise.reject(error);
}

// registering the custom error handler to the
// "api" axios instance
api.interceptors.response.use(undefined, (error) => {
    return errorHandler(error);
});
```

### axiosUtils.js
```javascript
export function defineCancelApiObject(apiObject) {
    // an object that will contain a cancellation handler
    // associated to each API property name in the apiObject API object
    const cancelApiObject = {}

    // each property in the apiObject API layer object
    // is associated with a function that defines an API call

    // this loop iterates over each API property name
    Object.getOwnPropertyNames(apiObject).forEach((apiPropertyName) => {
        const cancellationControllerObject = {
            controller: undefined,
        }

        // associating the request cancellation handler with the API property name
        cancelApiObject[apiPropertyName] = {
            handleRequestCancellation: () => {
                // if the controller already exists,
                // canceling the request
                if (cancellationControllerObject.controller) {
                    // canceling the request and returning this custom message
                    cancellationControllerObject.controller.abort()
                }

                // generating a new controller
                // with the AbortController factory
                cancellationControllerObject.controller = new AbortController()

                return cancellationControllerObject.controller
            },
        }
    });

    return cancelApiObject
}
```


### codeAPI.js
```javascript
import { api } from "./configs/axiosConfigs";
import { defineCancelApiObject } from "./configs/axiosUtils";

export const CodeAPI = {
    getNat: async function(code, cancel = false) {
        return await api.request({
            url: `/api/code/NAT/${code}`,
            method: "GET",
            // retrieving the signal value by using the property name
            signal: cancel ? cancelApiObject['getNat'].handleRequestCancellation().signal : undefined,
        });
    },
    getTitle: async function(code, cancel = false) {
        return await api.request({
            url: `/api/code/DPK2/${code}`,
            method: "GET",
            // retrieving the signal value by using the property name
            signal: cancel ? cancelApiObject['getTitle'].handleRequestCancellation().signal : undefined,
        });
    },  
};

// defining the cancel API object for ProductAPI
export const cancelApiObject = defineCancelApiObject(CodeAPI);
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

