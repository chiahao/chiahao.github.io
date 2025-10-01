---
layout: post
title: "svn Show Last Revision"
date: 2023-03-16 14:38:00
category: svn
tags: [svn]
---

### List logs:  
#### order by date descending:  
#### show only 4 records

```shell
svn log -r HEAD:1 --limit 4
```

### Show changed files to some revision 

```shell
svn log --verbose -r 24
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


