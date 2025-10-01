---
layout: post
title: "svnkit Command Line on Ubuntu 22.04"
date: 2023-02-21 14:35:00
category: programming
tags: [ubuntu]
---

## Step 1. Download svnkit

Use `dpkg -L svnkit` to show files installed.  
The file `/usr/bin/jsvn` is our target.  

## Step 2. Change Script Content
Remove backslash before variable:
```bash
'\$JAVA_HOME'
```
to  
```bash
'$JAVA_HOME'
```

## Step 3. Download Extra Library
Save [lz4](https://mvnrepository.com/artifact/net.jpountz.lz4/lz4/1.3.0) to `/usr/share/svnkit/`.  

## Step 4. Change script 
Change  
```shell
CLASSPATH="/usr/share/svnkit/svnkit-cli.jar"
```
to
```shell
CLASSPATH="/usr/share/svnkit/*"
```

## Step 5. Allow Java TLSv1、MD5
/usr/lib/jvm/java version/java.security

Change  
```bash
jdk.certpath.disabledAlgorithms=MD2, MD5, RSA keySize < 1024
jdk.tls.disabledAlgorithms=SSLv3, RC4, MD5withRSA, DH keySize < 768
```
to:  
```bash
jdk.certpath.disabledAlgorithms=MD2, RSA keySize < 1024  
jdk.tls.disabledAlgorithms=SSLv3, RC4, DH keySize < 768
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


