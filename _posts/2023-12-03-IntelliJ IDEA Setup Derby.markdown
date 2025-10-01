---
layout: post
title: "IntelliJ IDEA Setup Derby"
date: 2023-12-03 14:39:00
category: intellij
tags: [intellij, idea]
---

1. Click the project and cretate a new folder;  
2. Right click the new folder, and select `New` -> `Data Source in Path`, like `derby`;  
3. On the right panel of the idea window, click the database icon to expand;  
4. Click the `+` icon -> `Data Source` -> `Apache Derby`;  
5. Name: `Apache Derby (Embedded)`  
Path: the path to the `derby`  
**Must check the `Create Database`**,  
Or append `;create=true` to the end of url
6. Add derby driver to tomcat `lib` floder, literally copy all jar file to the folder.  
7. Add 
```xml
<Resource name="jdbc/ntnupmb"
   auth="Container"
   type="javax.sql.DataSource"
   maxTotal="100"
   maxIdle="30"
   maxWaitMillis="10000"
   driverClassName="org.apache.derby.jdbc.EmbeddedDriver"
   url="jdbc:derby:/Users/chiahao/Library/CloudStorage/Dropbox/ntnu/workspace/PersonCheckinSystem/testDb/derby"
   username="db"
   password="db"/>
```

P.S.  driver is `EmbeddedDriver`.
P.P.S. Must be deactive in `Database` Panel.
P.P.P.S. Jdk8 only support 10.14.2.0, version could be choozen on Driver tab.

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


