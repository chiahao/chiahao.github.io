---
layout: post
title: "Java Pattern Match"
date: 2022-05-13 16:02:00
category: java
tags: [java]
---

Use escape when there are parenthesis in regex.

```java
@Test
public void testRegexLongMatcher() {
	String user_agent = "Mozilla/5.0 (X11; Linux i686; rv:38.0) Gecko/20100101 Firefox/38.0";
	boolean expResult = false;
	boolean result = Pattern.compile("((X11; Linux i686; rv:38.0) Gecko/20100101 Firefox/38.0|(X11; Linux i686; rv:38.0) Gecko/20100101 Firefox/39.0)", Pattern.CASE_INSENSITIVE).matcher(user_agent).find();
	assertEquals(expResult, result);
}

@Test
public void testRegexLongMatcherWithParenthesisEscape() {
	String user_agent = "Mozilla/5.0 (X11; Linux i686; rv:38.0) Gecko/20100101 Firefox/38.0";
	boolean expResult = true;
	boolean result = Pattern.compile("(\\(X11; Linux i686; rv:38.0\\) Gecko/20100101 Firefox/38.0|\\(X11; Linux i686; rv:38.0\\) Gecko/20100101 Firefox/39.0)", Pattern.CASE_INSENSITIVE).matcher(user_agent).find();
	assertEquals(expResult, result);
}

```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


