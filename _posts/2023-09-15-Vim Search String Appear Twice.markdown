---
layout: post
title: "Vim Search String Appear Twice"
date: 2023-09-15 11:28:00
category: vim
tags: [vim]
---

```bash
/\(\w\+\).*return \1;  
```

✓ getIDNO(){return IDNO;}  
⤬ getNAME(){return "NAME";}

This will match first line, but not second line.

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


