---
layout: post
title: "Maven Execute Script In Clean Phase"
date: 2024-01-11 15:42:00
category: maven
tags: [maven]
---

```xml
<plugin>
   <groupId>org.codehaus.mojo</groupId>
   <artifactId>exec-maven-plugin</artifactId>
   <version>3.1.1</version>
   <executions>
      <execution>
         <id>setup_target</id>
         <phase>pre-clean</phase>
         <goals>
            <goal>exec</goal>
         </goals>
         <configuration>
            <executable>bash</executable>
            <commandlineArgs>setup_idea.sh</commandlineArgs>
         </configuration>
      </execution>
   </executions>
</plugin>

```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


