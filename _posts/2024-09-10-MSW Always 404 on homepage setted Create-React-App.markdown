---
layout: post
title: "MSW Always 404 on homepage setted Create-React-App"
date: 2024-09-10 15:32:00
category: programming
tags: [react, msw]
---

## Describe the bug

create-react-app with homepage setted causes MSW not to mock

## Environment

react: "^18.3.1"
msw: "^2.4.4"
nodejs: 21.1.0


## To Reproduce

1. npx create-react-app mytestapp
2. npm install msw@latest --save-dev
3. npx msw init public --save
4. Module not found: Error: Can't resolve 'graphql' in  
[ mockup msw doesn't work #82 ](https://github.com/mswjs/examples/issues/82)
>	Hey!
>	There are two things I recommend to solve this:
	
>	1. Use msw-storybook-addon.
>	2. Serve "public" since Storybook doesn't do that by default. I believe it's the "-p" flag in Storybook CLI.  

```shell
npm install --save graphql
```

5. mymswtestapp/src/mocks/browser.js

```javascript
import { setupWorker } from "msw/browser";
import { handlers } from "./handler";

export const worker = setupWorker(...handlers);
```

6. mymswtestapp/src/mocks/handler.js

```javascript
import { http, HttpResponse } from 'msw';

export const handlers = [
	http.post("api/code/NAT/:code", () => {
		return HttpResponse.json({
			"data": [
				{"CODE": "11", "DESCR": "UNIT1"},
				{"CODE": "22", "DESCR": "UNIT2"}
			]
		});
	}),

]
```
7. mymswtestapp/index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

async function enableMocking() {
	if (process.env.NODE_ENV !== 'development') {
		return;
	}

	const { worker } = await import("./mocks/browser");

	let workerService = worker.start();
	console.log(worker.listHandlers());
	return workerService;
}

enableMocking().then(() => {

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(
      <React.StrictMode>
        <App />
      </React.StrictMode>
    );
});
```

8. in firefox, send request 
`http://localhost:3000/api/code/NAT/1` can be succefully intercepted.

9. But add `"homepage": "myPage",` to `package.json` will cause problem.

10. Modify `mytestapp/index.js`: 

According to the issue [ Wrong url for mockServiceWorker.js when base config set in Vite 5.x config #2055 ](https://github.com/mswjs/msw/issues/2055) and [Using custom "homepage" property](https://mswjs.io/docs/recipes/using-custom-homepage) :   

```javascript
async function enableMocking() {
	if (process.env.NODE_ENV !== 'development') {
		return;
	}

	const packageJson = await import("../package.json");
	const { worker } = await import("./mocks/browser");

	// `worker.start()` returns a Promise that resolves
	// once the Service Worker is up and ready to intercept requests.
	let workerService = worker.start({
	    serviceWorker: {
	    	// Provide a custom worker script URL, taking
	    	// the "homepage" into account.
	    	url: `${packageJson.homepage}/mockServiceWorker.js`,
	    },
	});
}

enableMocking().then(() => {

const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(
      <React.StrictMode>
        <App />
      </React.StrictMode>
    );
});
```

11. Now `npm start` still can start server, and show `[MSW] Mocking enabled.`.  
But requests won't intercepted.

## Have studied 


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

