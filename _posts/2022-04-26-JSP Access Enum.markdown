---
layout: post
title: "JSP Access Enum"
date: 2022-04-26 13:46:00
category: java
tags: [java,jstl]
---


```java
public enum TheEnum {
	LOCALE_BASENAME("value1");

	private final String value;
	private TheEnum(final String value) {
		this.value = value;
	}
	public String toDbValue() {
		return value;
	}
}
```

Need to use page directive to import enum class:
```java
<@page import="mylib.myenums.TheEnum">

<c:if test="${'value1' eq TheEnum.LOCALE_BASENAME.toDbValue()}">
</c:if>
```

**ENUM** is supported until **EL 3.0**, i.e. Tomcat version 8.0.
| **Servlet Spec** | **JSP Spec** | **EL Spec** | **WebSocket Spec** | **Authentication (JASPIC) Spec** | **Apache Tomcat Version** | **Latest Released Version** | **Supported Java Versions**                |
| ---------------- | ------------ | ----------- | ------------------ | -------------------------------- | ------------------------- | --------------------------- | ------------------------------------------ |
| 3.1              | 2.3          | 3.0         | 1.1                | N/A                              | 8.0.x (superseded)        | 8.0.53 (superseded)         | 7 and later                                |
| 3.0              | 2.2          | 2.2         | 1.1                | N/A                              | 7.0.x (archived)          | 7.0.109 (archived)          | 6 and later<br>(7 and later for WebSocket) |
| 2.5              | 2.1          | 2.1         | N/A                | N/A                              | 6.0.x (archived)          | 6.0.53 (archived)           | 5 and later                                |


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


