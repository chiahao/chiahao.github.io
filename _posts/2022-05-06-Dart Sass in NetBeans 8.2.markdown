---
layout: post
title: "Dart Sass in NetBeans 8.2"
date: 2022-05-06 13:14:00
category: netbeans
tags: [netbeans]
---

According to [How to use Sass with NetBeans on Linux / macOS](https://stackoverflow.com/questions/52757589/how-to-use-sass-with-netbeans-on-linux-macos)  

> The issue is that --cache-location is no longer supported and should be removed. All of the original parameters are used by "$@". To remove the first two parameters, you should be able to use "${@:3}" (see Process all arguments except the first one (in a bash script)), but somehow that resulted into a "Bad substitution" error for me. So I opted to use shift 2 to remove them:


#### macOS (node.js)

create:

```shell
/usr/local/lib/node_modules/sass/sass_nb.sh
```

```shell
#!/bin/zsh

export PATH="$PATH:"/usr/local/bin/
shift 3
sass ${@}
```




[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


