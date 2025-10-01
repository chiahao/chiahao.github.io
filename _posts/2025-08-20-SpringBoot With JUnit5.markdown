---
layout: post
title: "SpringBoot With JUnit5"
date: 2025-08-20 10:24:00
category: program
tags: [springboot, junit5]
---

```xml
<dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.platform</groupId>
            <artifactId>junit-platform-commons</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.vintage</groupId>
            <artifactId>junit-vintage-engine</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.platform</groupId>
            <artifactId>junit-platform-launcher</artifactId>
            <scope>test</scope>
        </dependency>  
    </dependencies>
    <dependencyManagement>
        <dependencies>
            <dependency>  
                <groupId>org.junit</groupId>
                <artifactId>junit-bom</artifactId>
                <version>5.12.2</version>
                <type>pom</type>  
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

