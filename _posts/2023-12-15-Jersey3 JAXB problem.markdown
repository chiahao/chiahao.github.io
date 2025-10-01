---
layout: post
title: "-Jersey3 JAXB problem"
date: 2023-12-15 14:33:00
category: jersey3
tags: [jersey3, fasterxml]
---

[HK2 failure has been detected in a code that does not run in an active Jersey Error scope](https://stackoverflow.com/questions/38530282/hk2-failure-has-been-detected-in-a-code-that-does-not-run-in-an-active-jersey-er)

The error message is not the same as mine.  


```java

```

#### method 3:  

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>3.2.3</version>
    <configuration>
        <argLine>--add-modules=java.xml.bind</argLine>
    </configuration>
</plugin>
```
output error:  

```java
[ERROR] Error occurred during initialization of boot layer
[ERROR] java.lang.module.FindException: Module java.xml.bind not found
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


