---
layout: post
title: "Change Maven's Remote Repository in NetBeans8"
date: 2022-05-11 23:46:00
category: netbeans
tags: [netbeans, maven]
---


[https://stackoverflow.com/questions/60031044/how-to-change-mavens-remote-repository-url-in-the-netbeans-ide-from-http-to-ht](How to change maven's Remote Repository URL in the NetBeans IDE (from http to https)?)

> Goto Netbeans installation folder > java > maven > conf, and here I updated the settings.xml file using administrative privilege.
> as http repo link will not work now, just I created an mirror for central repo that is pre-built with IDE which cannot be changed.
> Add this inside mirrors tag of `settings.xml`

```xml
<mirror>
      <id>mirror1</id>
      <mirrorOf>central</mirrorOf>
      <name>mirror1</name>
      <url>https://repo.maven.apache.org/maven2/</url>
</mirror>
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


