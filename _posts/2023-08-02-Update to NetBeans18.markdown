---
layout: post
title: "Update to NetBeans18"
date: 2023-08-02 10:22:00
category: netbeans
tags: [netbeans]
---


#### Why Abandon NetBeans16?
[Downloading Apache NetBeans 16](https://netbeans.apache.org/download/nb16/)  
> Known Issues
> Gradle projects in Apache NetBeans 16 are currently not supported when running the IDE on JDK 19.

#### Safe to Use NetBeans18?
[Downloading Apache NetBeans 18](https://netbeans.apache.org/download/nb18/)  
> The Apache NetBeans 18 binary releases require JDK 11+, and officially support running on JDK 11, 17 and 20.


#### Dark mode
匯入 [Dracula](https://draculatheme.com/netbeans), 來指定字型等設定;  
視窗的外觀則用內建的:  
Apperance -> Look and Feel -> Preferred look and feel:  
下拉選擇 `FlatLaf Dark`  

#### Tomcat
不知道為什麼, 按了新增後, 電腦整個沒有回應超久。  
還好過了很久還是有進到下一頁, 
如果沒有勾選「Create user if it does not exist」, 就要手動去改 tomcat-users.xml.

#### CSS Preprocessor

change default:  
```bash
/usr/local/bin/sass
```

to  
/opt/dart-sass/sass


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


