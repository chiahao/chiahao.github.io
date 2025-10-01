---
layout: post
title: "Undo Git Commit amend"
date: 2024-09-05 09:47:00
category: programming
tags: [git]
---

### [How to Undo "git commit –amend"](https://www.baeldung.com/ops/git-commit-ammend-undo#:~:text=In%20short%2C%20we%20can%20undo,hard%20HEAD%40%7B1%7D%20command.)

```shell
git reset --soft HEAD@{1}
```

> Using the Git amend command (git commit –amend), we can change the message of a commit or even its content. But when we amend (or modify) something, it becomes a new thing, right? Therefore, when we change the message or content of a Git commit, the original commit is replaced by a new commit containing the changes.
> 
> Actually, after a Git amendment, we’ll still have just one commit containing all our combined content, but with a different hash. In practice, Git makes the old commit private and creates a new public one.
> 
> This is great news, as it means we can completely undo the effects of a Git amendment. However, we need to know how to reference the old commit properly so that we can undo the amendments.



> we can consult the detailed history of commits via the Git reflog:
```shell
$ git reflog
3499867 (HEAD -> feature1) HEAD@{0}: commit (amend): My updated commit message
400071c HEAD@{1}: commit: My original commit message
...
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

