---
layout: post
title: "Misuse of Java8 Optional"
date: 2022-03-09 08:36:00
category: java
tags: [java]
---

1. The intent of Java when releasing Optional was to use it as a return type
2. The practice of using `Optional` as a method parameter is even [discouraged by some code inspectors.](https://rules.sonarsource.com/java/RSPEC-3553)

```java
public staic List<Person> search(List<Person> people, String name, Optional<Integer> age) {
	// Null checks for people and name
	return people.stream()
			.filter(p -> p.getName().equals(name))
			.filter(p -> p.getAge().get() >= age.orElse(0))
			.collect(Collectors.toList());
}
```

And another developer tries to use it:
```java
someObject.search(people, "Peter", null);
// gets a NullPointerException!
```




[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


