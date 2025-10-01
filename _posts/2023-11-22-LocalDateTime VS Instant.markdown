---
layout: post
title: "LocalDateTime VS Instant"
date: 2023-11-22 09:37:00
category: java
tags: [java]
---

1. Instant represents a moment, a specific point in the timeline.  
2. LocalDateTime represents a date and a time-of-day. But lacking a time zone or offset-from-UTC, this class cannot represent a moment. It represents potential moments along a range of about 26 to 27 hours, the range of all time zones around the globe. A LocalDateTime value is inherently ambiguous.


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


