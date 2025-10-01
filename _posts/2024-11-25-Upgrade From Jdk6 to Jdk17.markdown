---
layout: post
title: "Upgrade From Jdk6 to Jdk17"
date: 2024-11-25 10:59:00
category: git
tags: [git]
---

# From Jdk6 to Jdk17   
若有錯誤, 請修正後分享。

# Customizing Maven Clean Plugin for target Directory
如果有用同步程式, 可能會先設定`target`目錄不要同步。  
但是`mvn clean`預設會刪除再重新建立`target`目錄, 導致不要同步的旗標會消失。  
下方設定, 能避免`mvn clean`刪除`target`目錄。

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-clean-plugin</artifactId>
            <version>3.3.2</version>
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
# Using JARs from Others Directly
有時會想直接想用別人的 jar 檔,   
這個 plugin 可以用`mvn clean`就用`lib`目錄裡的檔案自動更新本機 mvn repository 的檔案:
```xml
<plugin>
   <groupId>org.apache.maven.plugins</groupId>
   <artifactId>maven-install-plugin</artifactId>
   <version>2.5.2</version>
   <executions>
      <execution>
      <id>install_org_story</id>
      <phase>clean</phase>
          <goals>
              <goal>install-file</goal>
          </goals>
          <configuration>
             <groupId>org.story</groupId>
             <artifactId>story</artifactId>
             <version>1.0</version>
             <packaging>jar</packaging>
             <file>${basedir}/lib/Some.jar</file>
          </configuration>
      </execution>
   </executions>
</plugin>
```


# Codebase Compatibility
## Unsupported Java 6 APIs.
e.g. `sun.misc` packages

### encoder
```java
String encodedBytes = new sun.misc.BASE64Encoder().encode("exampleString")
```
改成:   
```java
String encodedBytes = Base64.getMimeEncoder().encodeToString("exampleString")
```

### decoder
```java
byte[] decodedBytes = new sun.misc.BASE64Decoder().decodeBuffer("exampleString")
```
改成:   
```java
byte[] decodedBytes = Base64.getMimeDecoder().decode("exampleString");
```



# Tomcat10 Handles UTF-8 Encoding by Default
不要再轉成`ISO-8859-1`:
```java
transNo = request.getParameter("TRANSNO");
transNo = new String(transNo.getBytes("ISO-8859-1"), "UTF-8");
```

# Date and Time Handling

## Legacy Code Using Joda-Time
*Joda* 官網也是寫要改用 *Java8* 內建的時間API。  

> Note that from Java SE 8 onwards, users are asked to migrate to java.time (JSR-310) - a core part of the JDK which replaces this project.
-- [www.joda.org](www.joda.org)

但是 *Java8* 之後還是沒有 *JodaTime* 的 `Interval`, 
可以考慮使用 `threeten-extra` 的 `Interval`.   
```xml
<dependency>
  <groupId>org.threeten</groupId>
  <artifactId>threeten-extra</artifactId>
  <version>1.8.0</version>
</dependency>
```

# DisplayTag Compatibility
`web.xml` 裡的 display filter 移除
```xml
<filter-class>org.displaytag.filter.ResponseOverrideFilter</filter-class>
```

# java.awt.Font
```java
Font font=new Font("字型",Font.TRUETYPE_FONT, 12);
```
改成建立後再指定字型大小
```java
InputStream fontStream = getClass().getResourceAsStream("/edukai-5.0.ttf");
Font font = Font.createFont(Font.TRUETYPE_FONT, fontStream).deriveFont(12f);
```

# POI

## 儲存格
```java
cellStyle.setBorderTop(CellStyle.BORDER_THIN);
cellStyle.setBorderRight(CellStyle.BORDER_THIN);
cellStyle.setBorderBottom(CellStyle.BORDER_THIN);
cellStyle.setBorderLeft(CellStyle.BORDER_THIN);
cellStyle.setAlignment(HSSFCellStyle.ALIGN_CENTER);
cellStyle.setVerticalAlignment(HSSFCellStyle.VERTICAL_CENTER);
```
改成:  

```java
cellStyle.setBorderTop(BorderStyle.THIN);
cellStyle.setBorderRight(BorderStyle.THIN);
cellStyle.setBorderBottom(BorderStyle.THIN);
cellStyle.setBorderLeft(BorderStyle.THIN);
cellStyle.setAlignment(HorizontalAlignment.CENTER);
cellStyle.setVerticalAlignment(VerticalAlignment.CENTER);
```

## 字型相關
```java
font.setColor(HSSFColor.BLACK.index);
font.setBoldweight(Font.BOLDWEIGHT_BOLD);
```
改成:  

```java
font.setColor(HSSFColor.HSSFColorPredefined.BLACK.getIndex());
font.setBold(true);
```


# Legacy Documents Resolved a Testing Discrepancy
最好還是要有原本的設計文件,  
業務單位測試以為匯出的報表會有日期欄位,  
但是查看程式, 真的就特地略過日期欄位。   
還好他手邊有之前印過的, 才想起來是那個功能很特別,
就是不會有日期欄位, 是隔壁的按鈕才會有。 

# (Optional) Using Git for Project Organization
## `git-svn`
因為不想在**本機**分不同目錄儲存 **Jdk6**, **Jdk17** 版本,  
所以請教周組長後, 試著用`git-svn`來操作。
但是目前懂的不多,  
無法提供協助, **請斟酌使用**。

1. Clone from svn
```shell
git svn init https://svn-server/svn/personnel_matters --trunk=PrivLib --branches=MavenizeProjects/{PrivLib} PrivLib
```

2. Setting the authorsfile

```bash
git config svn.authorsfile ~/authors.txt
```

3. Edit content of `.git/config`:    

```bash
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false  
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[svn-remote "svn"]
    url = https://svn-server/svn/personnel_matters
    fetch = PrivLib:refs/remotes/origin/trunk
    branches = MavenizeProjects/{PrivLib}/*:refs/remotes/origin/*
[svn]
    authorsfile = ~/authors_PmbMgr.txt
```

Modify these line:  
```xml
fetch = PrivLib:refs/remotes/origin/trunk
branches = MavenizeProjects/{PrivLib}/*:refs/remotes/origin/*
```  

to

```xml
fetch = PrivLib:refs/remotes/git-svn/trunk
branches = MavenizeProjects/{PrivLib}:refs/remotes/feature-jdk17/*
```

4. fetch

```shell
git svn fetch
```

might need to expand log size:  

```shell=zsh
git svn fetch --log-window-size=6500
```


5. checkout `feature-jdk17/PrivLib`

```xml
Note: switching to 'feature-jdk17/PrivLib'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 08b92ec jdk17版: 已同步原 jdk6 的 r5161
➜  ~/Downloads/PrivLib git:(08b92ec) git branch
➜  ~/Downloads/PrivLib git:(08b92ec) 
```

6. switch -c

```bash
git switch -c feature-jdk17
```

7. 合併
**不可以**在`master`直接`merge`或`rebase` *feature-jdk17* !  
會導致`master`的`svn`*metadata* 被覆蓋。  
目前只會用`cherry-pick`的非正規方式合併。  
如果有找到方法, 觀迎分享。

```bash
git cherry-pick master..feature-jdk17
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

