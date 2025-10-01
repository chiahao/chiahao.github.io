---
layout: post
title: "Psi-Probe Installation"
date: 2024-10-18 08:48:00
category: java
tags: [probe, tomcat]
---

When deploy to localhost, url would be directed to `localhot:8334/probe`  

1. Decompress the project:  
```shell
jar xvf probe.war
```

2. edit **probe/WEB-INF/web.xml**:  

```xml
<security-constraint>
	...
	<!-- remove these  
	<user-data-constraint>
	      <transport-guarantee>CONFIDENTIAL</transport-guarantee>
	</user-data-constraint>
	-->
</security-constraint>
```

3. Compress back to war file:  
```shell
cd probe
jar cvf probe.war *
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

