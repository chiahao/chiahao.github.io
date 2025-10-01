---
layout: post
title: "Vim Delete Words Without Matching"
date: 2025-01-10 08:22:00
category: program
tags: [vim]
---

## Ref: [In Vim how to delete all words and characters not matching a pattern](https://superuser.com/questions/559531/in-vim-how-to-delete-all-words-and-characters-not-matching-a-pattern)

```bash
:%s/\v(.*)(someting to match)(.*)/\2
```

> `\v`  
>  
> The "very magic" flag is useful for limiting the number of backslashes and improve legibility.  
> `(.*)`
>  
>  The first group contains any number of any character. Anchoring to the start of the line is implied so it matches whatever is before what you want. It would be `\(.*\)` without the "very magic" flag.



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

