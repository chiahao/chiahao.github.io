---
layout: post
title: "Tomcat Process sendError"
date: 2025-04-29 10:52:00
category: program
tags: [java]
---

```java
// Tomcat still return full HTML thing.
response.sendError(((CustomizedException) ex).getHttpStatusCode(), ex.getMessage());  
return;  

// Adopt this:
response.setStatus(((CustomizedException) ex).getHttpStatusCode()); // 409
response.setContentType("text/plain;charset=UTF-8");
response.getWriter().write(ex.getMessage()); // E0002
return;
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

