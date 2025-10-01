---
layout: post
title: "MSW Troubleshooting"
date: 2024-11-26 16:22:00
category: program
tags: [msw]
---

Upgrade MSW to 2.6.6.

```xml
The operation is insecure.
getWorkerInstance@http://localhost:3000/static/js/vendors-node_modules_msw_lib_browser_index_mjs-node_modules_msw_lib_core_HttpResponse_mjs-nod-8fd840.chunk.js:5736:11
```

AI Suggests to put **mockServiceWorker.js** into **/public/myPage/mockServiceWorker.js**  

```xml
 url: "/myoage/mockServiceWorker.js",
+
/public/mypage/mockServiceWorker.js
	All Fail!  
	http://localhost:3000/mypage
	http://localhost:3000/mypage/
	http://localhost:3000/myPage/mypage
	http://localhost:3000/myPage/mypage/
```
```xml
url: "mypage/mockServiceWorker.js",
+
/public/mypage/mockServiceWorker.js
	http://localhost:3000/mypage
		Not work!
	http://localhost:3000/mypage/
		Work
		But api still 404
```
```xml
url: "mypage/mockServiceWorker.js",
+
/public/mockServiceWorker.js
	http://localhost:3000/myPage
		Not work!
	http://localhost:3000/myPage/
		Work
```
```xml
url: "/mypage/mockServiceWorker.js",
+
/public/mockServiceWorker.js
	http://localhost:3000/myPage
		❌
	http://localhost:3000/myPage/
		❌
	Comfirmed url starts '/' would fail!  
```
```xml
index.js
url: "mypage/mockServiceWorker.js",
"msw": {"workerDirectory": ["public"]},
+
/public/mypage/mockServiceWorker.js
	http://localhost:3000/mypage
		Not work!
	http://localhost:3000/mypage/
		Work
```
```xml
index.js
url: "mypage/mockServiceWorker.js",
"msw": {"workerDirectory": ["public"]},
+
/public/mockServiceWorker.js
	http://localhost:3000/mypage
		Work
	http://localhost:3000/mypage/
		Not work!
```
```xml
index.js
url: "/mockServiceWorker.js",
"msw": {"workerDirectory": ["public"]},
+
/public/mockServiceWorker.js
	http://localhost:3000/
		❌
	http://localhost:3000/mypage
		❌
	http://localhost:3000/mypage/
		❌
```
```xml
index.js
url: "mypage/mockServiceWorker.js",
"msw": {"workerDirectory": ["public/mypage"]},
+
/public/mypage/mockServiceWorker.js
	http://localhost:3000/mypage
		❌
	http://localhost:3000/mypage/
		✅
```
```xml
index.js
url: "mypage/mockServiceWorker.js",
"msw": {"workerDirectory": ["public/mypage/"]},
+
/public/mypage/mockServiceWorker.js
	http://localhost:3000/mypage
	http://localhost:3000/mypage/
```
```xml
index.js
url: "mockServiceWorker.js",
"msw": {"workerDirectory": ["public/mypage"]},
+  
/public/mypage/mockServiceWorker.js
	http://localhost:3000/mypage  
		❌
	http://localhost:3000/mypage/  
		❌
	http://localhost:3000/mypage/mypage
		✅
	It works when api changed to **/mypage/mypage/api**.  
		✅
```

## Final Work Version!  
URL must be `http://localhost:3000/mypage/`, the last `/` is necessary!  

```xml
index.js
url: "mockServiceWorker.js",
"msw": {"workerDirectory": ["public"]},
+  
/public/mockServiceWorker.js
```



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

