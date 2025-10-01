---
layout: post
title: "Git Commit Your Changes Or Stash Them Before You Merge"
date: 2022-03-19 15:45:00
category: git
tags: [git]
---

## Commit the changes
```shell
git commit -m "updating message"
```

## Stash
```shell
git stash
```
then merge:
```shell
git stash pop
```

## Discard the local changes
```shell
git reset --hard
```
or 
```shell
git checkout -t -f remote/branch
```
For spacific file
```shell
git checkout filename
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


