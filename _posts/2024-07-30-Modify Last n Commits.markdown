---
layout: post
title: "Modify Last n Commits"
date: 2024-07-30 15:11:00
category: programming
tags: [git]
---

[How do I modify a specific commit?](https://stackoverflow.com/questions/1186535/how-do-i-modify-a-specific-commit)

```sh
git rebase --interactive bbc643cd hashcode~
```

> **~** at the end of the command, because you need to reapply commits on top of the previous commit of `bbc643cd`.

> In the default editor, modify pick to edit in the line mentioning bbc643cd.


```sh
git commit --all --amend --no-edit
```

```sh
git rebase --continue
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

