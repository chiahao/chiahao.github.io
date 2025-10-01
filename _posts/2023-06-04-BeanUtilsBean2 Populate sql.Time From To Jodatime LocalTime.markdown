---
layout: post
title: "BeanUtilsBean2 Populate sql.Time From/To Jodatime LocalTime"
date: 2023-06-04 11:28:00
category: java
tags: [java]
---

```java
BeanUtilsBean2 beanUtilsBean = new BeanUtilsBean2();
beanUtilsBean.getConvertUtils().register(new Converter(){
    @Override
	public Object convert(Class type, Object value) {
		return new LocalTime(((Time) value));
	}
}, LocalDate.class);
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


