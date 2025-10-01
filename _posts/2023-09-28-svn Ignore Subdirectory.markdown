---
layout: post
title: "svn Ignore Subdirectory"
date: 2023-09-28 11:19:00
category: svn
tags: [svn]
---

1. Add parent folder first:  

```shell
svn add parent_folder_name
```

2. Delete but keep local:  

```shell
svn rm --keep-local subfolder_name
```

3. set `svn:ignore`:  

```shell
svn propedit svn:ignore parent_folder_name
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


