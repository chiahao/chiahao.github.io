---
layout: post
title: "Javascript Create Array From 1 to N"
date: 2022-02-15 09:39:00
category: program
tags: [javascript]
---

## [How to create an array containing 1...N](https://stackoverflow.com/questions/3746725/how-to-create-an-array-containing-1-n)

```javascript
Array.from(Array(10).keys());
// => [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```
```javascript
[...Array(10).keys()]
// => [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```
```javascript
Array.from({length: 10}, (_, i) => i + 1)
//=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```
```javascript
[...Array(N+1).keys()].slice(1)
```

spread operator (...)

```javascript
var foo = Array(N).fill().map((v,i)=>i);
```

even:  
```javascript
Array.from({length: 10}, (_, i) => i * 2);
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

