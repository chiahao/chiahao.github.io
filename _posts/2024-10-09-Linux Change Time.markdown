---
layout: post
title: "Linux Change Time"
date: 2024-10-09 09:08:00
category: linux
tags: [linux]
---


```shell
/bin/date
/sbin/hwclock --systohc --localtime
/usr/bin/ntpdate

/usr/sbin/crond


/bin/date +%Y%M%D -s 20161201
ntpdate -s 140.122.8.254
```

**~/.profile**  

```shell
TZ=‘Asia/Taipei’;export TZ
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

