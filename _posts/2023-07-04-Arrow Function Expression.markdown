---
layout: post
title: "Arrow Function Expression"
date: 2023-06-30 08:08:00
category: html
tags: [html]
---

### [Arrow function expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

1. Arrow function don't have their own bindings to `this`, `arguments`, or `super`, and sould not be used as `methods`.
2. Arrow function cannot be used as constructors.  Calling them the `new` throws a `TypeError`.  They also don't have access to the `new.target` keyword.
3. Arrow functions cannot use `yield` within their body and cannot be created as generator functions.

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


