---
layout: post
title: "Vim Only Keep Some Characters"
date: 2025-05-23 11:44:00
category: program
tags: [mockito]
---

```java

-- Original method  
public String updateTotalPayTemporaryHourly(int form_sn) 

-- fail!  
when(formDao.updateTotalPayTemporaryHourly(any())).thenReturn("");
```

only mock object, so `updateTotalPayTemporaryHourly(int)` will fail.  

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

