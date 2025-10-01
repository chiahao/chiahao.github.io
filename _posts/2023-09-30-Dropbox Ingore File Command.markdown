---
layout: post
title: "Dropbox Ingore File Command"
date: 2023-09-30 11:19:00
category: dropbox
tags: [dropbox]
---

1. For Mac  

```shell
xattr -w 'com.apple.fileprovider.ignore#P' 1 FOLDER_NAME
```

without FileProvider:  

```shell
xattr -w com.dropbox.ignored 1 FOLDER_NAME
```

2. For Ubuntu  

```shell
attr -s com.dropbox.ignored -V 1 FOLDER_NAME
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


