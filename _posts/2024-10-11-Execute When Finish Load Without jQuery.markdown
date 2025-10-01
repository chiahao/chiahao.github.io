---
layout: post
title: "Execute When Finish Load Without jQuery"
date: 2024-10-11 07:48:00
category: html
tags: [html, javascript, jquery]
---

## [Replacing Query with Vanilla JavaScript](https://dev.to/rfornal/-replacing-jquery-with-vanilla-javascript-1k2g)  

// With jQuery
```javascript
$(document).ready(function() { 
  /* Do things after DOM has fully loaded */
});
```

// Without jQuery
```javascript
const onReady = (callback) =>{
  if (document.readyState!='loading') callback();
  else if (document.addEventListener) document.addEventListener('DOMContentLoaded', callback);
  else document.attachEvent('onreadystatechange', function() {
    if (document.readyState=='complete') callback();
  });
};

ready(() => { 
  /* Do things after DOM has fully loaded */ 
});
```


## [Cheat sheet for moving from jQuery to vanilla JavaScript](https://tobiasahlin.com/blog/move-from-jquery-to-vanilla-javascript/)

// With jQuery
```javascript
$(document).ready(function() { 
  /* Do things after DOM has fully loaded */
});
```

// Without jQuery
// Define a convenience method and use it
```javascript
var ready = (callback) => {
  if (document.readyState != "loading") callback();
  else document.addEventListener("DOMContentLoaded", callback);
}

ready(() => { 
  /* Do things after DOM has fully loaded */ 
});
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

