---
layout: post
title: "Javascript Date Plus One Day"
date: 2023-03-27 16:09:00
category: javascript
tags: [javascript]
---

```javascript
var start_date = new Date();
var afterOneDay = new Date(start_date.getTime() + 24 * 60 * 60 * 1000);
```

### Date.now()
The Date.now() static method returns the number of milliseconds elapsed since the epoch, which is defined as the midnight at the beginning of January 1, 1970, UTC.

### getTime()
> The getTime() method returns the number of milliseconds since the epoch, which is defined as the midnight at the beginning of January 1, 1970, UTC.

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


