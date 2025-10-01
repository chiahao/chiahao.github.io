---
layout: post
title: "Install Ubuntu 22.04"
date: 2023-01-12 14:35:00
category: programming
tags: [ubuntu]
---

還好這次沒有像 Ubuntu 18.04 升到 20.04 時一樣大改,  
所以一些設定還是可以延用。

比較痛苦的是開發工具居然都無法從官方網站下載了!  


#### gvim letter spacing problem

```xml
" 註解掉預設字型
" set guifont=Osaka-Mono:h21
" 目前改用這個字型看起來比較順眼
set guifont=DejaVu\ Sans\ Mono\ 10
```

使用 NetBeans 內建的 svn 時, 需要允許 `MD5`,  
自 java8 後, 就不支援  
http://stackoverflow.com/questions/14149545/java-security-cert-certificateexception-certificates-does-not-conform-to-algori  
java.security file is located in linux 64 at Library/Java/JavaVirtualMachines/jdk1.8.0_45.jdk/Contents/Home/jre/lib/security/java.security

```bash
original keys
jdk.certpath.disabledAlgorithms=MD2, MD5, RSA keySize < 1024
jdk.tls.disabledAlgorithms=SSLv3, RC4, MD5withRSA, DH keySize < 768
change to
jdk.certpath.disabledAlgorithms=MD2, RSA keySize < 1024
jdk.tls.disabledAlgorithms=SSLv3, RC4, DH keySize < 768
```

## Create .Desttop in App Launcher



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


