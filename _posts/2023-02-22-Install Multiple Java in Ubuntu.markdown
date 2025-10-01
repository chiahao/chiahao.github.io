---
layout: post
title: "Install Multiple Java in Ubuntu"
date: 2023-02-22 09:59:00
category: programming
tags: [ubuntu]
---

```bash
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-19.0.2/bin/java
sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-19.0.2/bin/javac
sudo update-alternatives --install /usr/bin/jar jar /usr/lib/jvm/jdk-19.0.2/bin/jar
```



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


