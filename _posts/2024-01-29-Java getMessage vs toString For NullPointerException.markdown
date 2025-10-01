---
layout: post
title: "Java getMessage vs toString For NullPointerException"
date: 2024-01-29 15:05:00
category: java
tags: [java]
---

```java
@Test
public class testNullPointerException {
    Throwable expectedException = assertThrow(NullPointerException.class, () -> {
        throw new NullPointerException();
    });
    assertAll("Expect NullPointerException.getMessage() is Null; .toString() is 'null'"
        assertNull(expectedException.getMessage());
        assertEquals("", expectedException.toString());
    );
}
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

