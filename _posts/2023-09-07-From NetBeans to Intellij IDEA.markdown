---
layout: post
title: "From NetBeans to Intellij IDEA"
date: 2023-09-07 14:39:00
category: intellij
tags: [intellij, idea]
---

https://www.youtube.com/watch?v=-Y4uiikR-EE

有教到很重要的一點
1. 先建立 modules
選擇專案後, 按 + 號, 選 web
就會在專案下增加一個有特別 web
2. 增加 artificate
選 Web Application: Exploded, 
因為有做第一步, 這邊才會有第二個子選項: 
From Modules
3. 再到 tomcat 設定 configuration
選單 Run -> Edit Configurations
4. 選到 tomcat 6 後, 選右邊的 頁籤：Deployment, 就可以加入剛才的 專案
5. 下面的 Application Context 記得去掉不必要的字, e.g. PmbMgr.war.blalba

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


