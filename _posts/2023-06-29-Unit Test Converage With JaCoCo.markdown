---
layout: post
title: "Unit Test Converage With JaCoCo"
date: 2023-06-29 14:32:00
category: jacoco
tags: [unittest, jacoco]
---

[Intro to JaCoCo](https://www.baeldung.com/jacoco)

In NetBeans16, we could just include following plugin to get code coverage.  
Right click on the project, the menu would show function: code coverage.  

```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.8</version>
    <executions>
        <execution>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>prepare-package</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


