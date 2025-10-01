---
layout: post
title: "RESTful Redirect URL"
date: 2025-05-12 10:58:00
category: rest
tags: [rest]
---

```java
String contextPath = request.getContextPath();  // e.g., "/AttendApply"
targetURL = contextPath + "/" + targetURL;
return Response.seeOther(URI.create(targetURL)).build();
```

Because root of api is `/api`:  

```java
@ApplicationPath("/api")
public class RestApplication extends Application {  
}
```

If just use `Response.seeOther(targetURL).build()` would be `api/targetURL` not just `targetUrl`.  

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


