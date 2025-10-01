---
layout: post
title: "git-svn Complain Malformed network data"
date: 2024-04-26 11:04:00
category: programming
tags: [git]
---

```xml
Found possible branch point: https://140.122.66.77/svn/personnel_matters/PdbLib => https://140.122.66.77/svn/personnel_matters/PbdLib, 206  
Error from SVN, (175009): Malformed network data: The XML response contains invalid XML: Malformed XML: no element found at line 1
```


Ref.:  [Getting error while migrating code from svn to git repository: Malformed network data: The XML response contains invalid XML: svn2git](https://stackoverflow.com/questions/38071052/getting-error-while-migrating-code-from-svn-to-git-repository-malformed-network)   
This make git start to download!  
```shell
git svn fetch --log-window-size=6000
```



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

