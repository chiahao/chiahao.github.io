---
layout: post
title: "Migrate From Jodatime to Java Time"
date: 2024-05-03 13:57:00
category: programming
tags: [java]
---


|----|JodaTime|Java Time|
|----|-----|-----|
|day of week |LocalDate.dayOfWeek() |.getDayOfWeek() |
|date to datetime|LocalDate.toDateTimeAtStartOfDay() |.atStartOfDay() | 
|time to datetime|LocalDate.toDateTimeToday() |.atDate(LocalDate date) | 




[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

