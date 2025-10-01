---
layout: post
title: "Optional as a Record Parameter in Java"
date: 2024-09-26 10:03:00
category: programming
tags: [java]
---

### [Optional as a Record Parameter in Java](https://www.baeldung.com/java-record-optional-param)


```java
public record Product(String name, double price, Optional<String> description) {
}
```



```java
public record User(String username, String email, String phoneNumber) {
    public Optional<String> getOptionalPhoneNumber() {
        return Optional.ofNullable(phoneNumber);
    }
}
```



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

