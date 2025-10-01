---
layout: post
title: "JAXRS Code Defined In External Jar"
date: 2023-10-26 11:49:00
category: react
tags: [react]
---

1. The class must be annotated `@Path`

2. `WEB-INF/web.xml`:  
```xml
<servlet>
	<servlet-name>jersey-servlet</servlet-name>
	<servlet-class>org.glassfish.jersey.servlet.ServletContainer</servlet-class>
	<init-param>
		<param-name>jersey.config.server.provider.packages</param-name>
		<param-value>rainbow.personcheckin.controller;rainbow.personcheckin.rest</param-value>
	</init-param>
	<load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
	<servlet-name>jersey-servlet</servlet-name>
	<url-pattern>/api/*</url-pattern>
</servlet-mapping>
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


