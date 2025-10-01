---
layout: post
title: "NS_ERROR_NET_PARTIAL_TRANSFER AND include(req,resp)"
date: 2024-10-23 08:22:00
category: program
tags: [java]
---

```java
RequestDispatcher target = req.getRequestDispatcher("/WEB-INF/pages/index.jsp");
target.include(req, resp);
```

would cause `NS_ERROR_NET_PARTIAL_TRANSFER` in browser,  
But some browser still could show page, whereas others couldn't.  


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

