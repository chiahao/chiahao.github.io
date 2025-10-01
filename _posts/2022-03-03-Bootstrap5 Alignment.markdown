---
layout: post
title: "Bootstrap5 Alignment"
date: 2022-03-03 17:17:00
category: css
tags: [bootstrap]
---

> Columns build on the grid’s flexbox architecture.
> Flexbox means we have options for changing individual columns and modifying groups of columns at the row level.
> You choose how columns grow, shrink, or otherwise change.
> 
> When building grid layouts, all content goes in columns. The hierarchy of Bootstrap’s grid goes from container to row to column to your content. On rare occasions, you may combine content and column, but be aware there can be unintended consequences.
> 
> Bootstrap includes predefined classes for creating fast, responsive layouts. With six breakpoints and a dozen columns at each grid tier, we have dozens of classes already built for you to create your desired layouts. This can be disabled via Sass if you wish.



## 1. vertical alignment
```html
<div class="row justify-content-start"></div>
<div class="row justify-content-end"></div>
<div class="row justify-content-center"></div>
<div class="row justify-content-between"></div>
<div class="row justify-content-evenly"></div>
```
```html
<div class="row">
	<div class="col align-self-start"></div>
	<div class="col align-self-center"></div>
	<div class="col align-self-end"></div>
</div>
```
```html
<div class="row">
	<div class="col align-self-start"></div>
	<div class="col align-self-center"></div>
	<div class="col align-self-end"></div>
</div>
```



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


