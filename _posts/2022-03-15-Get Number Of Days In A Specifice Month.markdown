---
layout: post
title: "Get Number Of Days In A Specifice Month"
date: 2022-03-15 10:25:00
category: javascript
tags: [javascript]
---

If day is 0, it will return the last day of last month.

```javascript
function getDays(year, month) {
	return new Date(year, month, 0).getDate();
}
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


