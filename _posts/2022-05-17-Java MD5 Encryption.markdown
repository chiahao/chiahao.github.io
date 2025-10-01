---
layout: post
title: "Java MD5 Encryption"
date: 2022-05-17 08:48:00
category: java
tags: [java]
---


```java
	byte[] digest = MessageDigest.getInstance("MD5").digest("The String");
	StringBuilder sb = new StringBuilder();
	// transform into hex
	for (byte b : digest) {
		sb.append(String.format("%02x", b));
	}
	String token = sb.toString();
```

```java
String.format(String format, Object... args)
```
```%[argument_index$][flags][width][.precision]conversion```

- argument_index: Optional.  Is a decimal integer indicating the position of the argument in the argument list. The first argument is referenced by "1$", the second by "2$", etc.
- flags: Optional.  Is a set of characters that modify the output format. The set of valid flags depends on the conversion.  If shorter than `width`, fill with `flags`.
- width: Optional.  Is a positive decimal integer indicating the minimum number of characters to be written to the output.
- precision: Optional.  Is a non-negative decimal integer usually used to restrict the number of characters. The specific behavior depends on the conversion.
- conversion: Required.  Is a character indicating how the argument should be formatted. The set of valid conversions for a given argument depends on the argument's data type.  `x` means hexadecimal format.


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


