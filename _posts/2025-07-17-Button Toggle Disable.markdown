---
layout: post
title: "Button Toggle Disable"
date: 2025-07-17 09:01:00
category: program
tags: [javascript]
---

```javascript

$('#pctp2_form button[name=submitBtn]').bind('click', disableClick, false);  
  
var disableClick = function () {
  return false;
};
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

