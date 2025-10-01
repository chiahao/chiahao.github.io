---
layout: post
title: "Json-Lib(net.sf.json) Serialize Jodatime LocalDate"
date: 2023-06-04 11:28:00
category: java
tags: [java]
---

```java
JsonConfig jsonConfig = new JsonConfig();
jsonConfig.registerJsonValueProcessor(LocalDate.class, new JsDateJsonValueProcessor() {
	@Override
	public Object processObjectValue(String key, Object value, JsonConfig jsonConfig) {
		return ((LocalDate) value).toString("yyyy-MM-dd");
	}
});

JSONObject.fromObject(resultMap, jsonConfig).toString();
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


