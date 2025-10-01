---
layout: post
title: "BeanUtilsBean2 Populate sql.Timestamp From/To Jodatime LocalDateTime"
date: 2023-06-04 11:28:00
category: java
tags: [jodatime]
---

```java
BeanUtilsBean2 beanUtilsBean = new BeanUtilsBean2();
beanUtilsBean.getConvertUtils().register(new Converter(){
    @Override
	public Object convert(Class type, Object value) {
		return LocalDateTime.fromDateFileds((Timestamp) value);
	}
}, LocalDateTime.class);
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


