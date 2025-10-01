---
layout: post
title: "Replace and Increment"
date: 2020-10-06 14:44:00
category: vi
tags: [vi,vim]
---

```bash
:let i=1 | g/Being Replaced/s//\="TheString".i."TheString"/ | let i=i+1
```

Only Replace the first match each line when there are multiple matches in one line.


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

