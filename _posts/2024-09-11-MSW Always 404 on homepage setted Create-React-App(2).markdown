---
layout: post
title: "MSW Always 404 on homepage setted Create-React-App(2)"
date: 2024-09-11 09:03:00
category: programming
tags: [react, msw]
---

Modified `browser.js`:  

```javascript
import { setupWorker } from "msw/browser";
import { handlers } from "./handler";

export const worker = setupWorker(...handlers);
worker.events.on('request:start', async ({ request }) => {
  // Read the request body as text for every request
  // that occurs in your application.
  const payload = await request.clone().text()
});

worker.events.on('request:start', ({ request }) => {
  console.log('Outgoing:', request.method, request.url)
});
```

Test the `homepage` not setting version:


But still once `homepage` being setted, the request is not intercepted:



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

