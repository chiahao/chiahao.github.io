---
layout: post
title: "Get Element Style width"
date: 2022-02-24 09:37:00
category: program
tags: [javascript]
---

## window.getComputedStyle()

> The Window.getComputedStyle() method returns an object containing the values of all CSS properties of an element, after applying active stylesheets and resolving any basic computation those values may contain.

> It's quite wrong to use ele.style.width to get the element's width!!!!!!
> In native JavaScript, you can get a element's CSS through two ways:
> ## Standard Method
> 
> ```javascript
> window.getComputedStyle(ele);
> ```
> 
> For example,
> ```javascript
> var ele = document.getElementById("content"), // Do not use #
>     eleStyle = window.getComputedStyle(ele);
> /* Below is the width of ele */
> var eleWidth = eleStyle.width;
> ```
> 
> ## Why Not Use ele.style?
> 
> ele.style is just get the attribule style of ele. If you use ele.style.width, you just get the width of ele.style, not the real width of ele.
> 
> If you have done something like:
> 
> ```javascript
> ele.style.width = "55px"
> ```
> You get "55px" when using ele.style.width. If you haven't, you will get undefined.

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

