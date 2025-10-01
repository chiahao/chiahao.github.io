---
layout: post
title: "Maven and Gradle Not To Delete target or build folder"
date: 2025-08-14 09:01:00
category: program
tags: [maven, gradle]
---

```xml

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-clean-plugin</artifactId>
            <version>3.0.0</version>
            <executions>
                <execution>
                    <id>Deleting all files under target, but not target itself</id>
                    <phase>clean</phase>
                    <goals>
                        <goal>clean</goal>
                    </goals>
                </execution>
            </executions>
            <configuration>
                <excludeDefaultDirectories>true</excludeDefaultDirectories>
                <filesets>
                    <fileset>
                        <directory>target/</directory>
                        <followSymlinks>false</followSymlinks>
                        <includes>
                            <include>**/*</include>
                        </includes>
                    </fileset>
                </filesets>
            </configuration>
        </plugin>
    </plugins>
</build>
```

```kts
tasks.named<Delete>("clean") {
    // 既定（buildDir自体）の削除対象を空に
    setDelete(emptyList<Any>())

    doFirst {
        val buildDirFile = layout.buildDirectory.get().asFile
        val children = buildDirFile.listFiles()?.toList() ?: emptyList()
        setDelete(children)
    }
}
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

