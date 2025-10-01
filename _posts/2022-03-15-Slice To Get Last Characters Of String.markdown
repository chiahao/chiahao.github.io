---
layout: post
title: "Slice To Get Last Characters Of String"
date: 2022-03-15 08:36:00
category: javascript
tags: [javascript]
---

## Syntax
The slice() method is a copying method.  
It does not alter this but instead returns a shallow copy that contains some of the same elements as the ones from the original array.

```javascript
slice()
slice(start)
slice(start, end)
```

*start*:  
if `start < 0`, `start + array.length` is used.  
if `start < -array.length` or `start` is omitted, `0` is used.  
if `start >= array.length`, nothing is extracted.  

*end*: extracts up to but not including `end`.  
if `end < 0`, `end + array.length` is used.  
if `end < -array.length`, `0` is used.  
if `end >= array.length` or `end` is omitted, `array.length` is used, causing all elements until the end to be extracted.  
if `end` is positioned before or at `start ` after normalization, nothing is extracted.  





[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


