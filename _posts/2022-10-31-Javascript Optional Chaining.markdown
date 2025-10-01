---
layout: post
title: "Javascript Optional Chaining"
date: 2022-10-31 11:25:00
category: programming
tags: [javascript]
---

### Optional Chaining

```javascript
const adventurer = {
	name: "Alice",
	cat: {
		name: "Dinah"
	}
}

function* createName() {
	return "12"
}

console.log(adventurer.dog?.name);
// undefined
```

```javascript
adventurer.dog?.name = createName()
// Error: Left side of assignment is not a reference.
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


