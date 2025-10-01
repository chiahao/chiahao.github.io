---
layout: post
title: "Lombok Annotation Not Work In Jdk6 Maven Project"
date: 2023-06-29 15:29:00
category: java
tags: [lombok, jdk6]
---

In NetBeans8, the default compiler-plugin is **2.0.2**,  
Which is too old to let lombok to enable **Annoation Process**.  

The minimun version to allow  **Annoation Process** is **2.5.1**.  

```xml
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-compiler-plugin</artifactId>
	<version>2.5.1</version>
	<configuration>
		<source>1.6</source>
		<target>1.6</target>
		<encoding>UTF-8</encoding>
		<annotationProcessorPaths>
			<path>
				<groupId>org.projectlombok</groupId>
				<artifactId>lombok</artifactId>
				<version>1.18.10</version>
			</path>
		</annotationProcessorPaths>
	</configuration>
</plugin>
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-war-plugin</artifactId>
	<version>2.3</version>
	<configuration>
		<warName>${project.name}</warName>
	</configuration>
</plugin>
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


