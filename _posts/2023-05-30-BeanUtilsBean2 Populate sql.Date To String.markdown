---
layout: post
title: "BeanUtilsBean2 Populate sql.Date To String"
date: 2023-05-30 11:28:00
category: java
tags: [java]
---

```java
DateConverter converter = new DateConverter();
converter.setPattern("yyyy-MM-dd");
BeanUtilsBean2 beanUtilsBean = new BeanUtilsBean2();
beanUtilsBean.getConvertUtils().register(converter, java.sql.Date.class);
beanUtilsBean.populate(bean, temp);
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


