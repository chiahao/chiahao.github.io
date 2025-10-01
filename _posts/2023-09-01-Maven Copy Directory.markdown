---
layout: post
title: "Maven Copy Directory"
date: 2023-09-01 13:55:00
category: maven
tags: [maven]
---

```xml
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-resources-plugin</artifactId>
	<version>3.2.0</version>
	<executions>
		<execution>
			<id>copy-resource-one</id>
			<phase>generate-sources</phase>
			<goals>
				<goal>copy-resources</goal>
			</goals>
			<configuration>
				<outputDirectory>${basedir}/target/${project.name}</outputDirectory>
				<resources>
					<resource>
						<directory>${frontend.folder.name}/build</directory>
						<includes>
							<include>**/*</include>
						</includes>
					</resource>
				</resources>
			</configuration>
		</execution>
	</executions>
</plugin>
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


