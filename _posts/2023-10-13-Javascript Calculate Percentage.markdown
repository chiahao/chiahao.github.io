---
layout: post
title: "Javascript Calculate Percentage"
date: 2023-10-13 09:53:00
category: javascript
tags: [javascript]
---

```javascript
let num = (data[0] / (data[0] + data[1])) * 100;
if (num < 1) {
	return num.toFixed(1) + "%";
} else if (num < 10) {
	return num.toPrecision(2) + "%";
} else {
	return Math.floor(num) + "%";
}
```

The result would be 0.X%, 2.3%, 99%

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


