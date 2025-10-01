---
layout: post
title: "Git delete by us"
date: 2024-11-21 08:29:00
category: git
tags: [git]
---

# [GIT: How dangerous is "deleted by us" conflict?](https://stackoverflow.com/questions/42174485/git-how-dangerous-is-deleted-by-us-conflict)

> someone deleted this file in the master branch on which you are rebasing new_branch.
> Assuming that the delete has not yet been staged and you want to keep this file, then you should git add the file to mark it that it should be kept:
> ```bash
> git add app/file.php
> ```
> Then, resolve all other merge conflicts and do git rebase --continue

> Note that if you wanted to accept the delete you would do git rm instead.

Comments:  
> "deleted by us" means it was deleted by "them"? – xaxxon  

> See this [canonical answer](https://stackoverflow.com/questions/21025314/who-is-us-and-who-is-them-according-to-git) for an explanation. In a rebase, "us" becomes the branch against which you are applying the commits, which is when the merge conflict due to the deleted file occurs. – Tim Biegeleisen


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

