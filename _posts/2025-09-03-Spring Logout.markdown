---
layout: post
title: "Spring Redirect and Fowrward"
date: 2025-08-26 11:08:00
category: program
tags: [spring, junit5]
---


### 303/302 return
```java
@Bean
@Order(2)
SecurityFilterChain publicChain(HttpSecurity http, TokenManager tokenManager) throws Exception {
	http
			.securityMatcher("/**")
			.csrf(AbstractHttpConfigurer::disable)
			.cors(AbstractHttpConfigurer::disable)
			.formLogin(AbstractHttpConfigurer::disable)
			.logout(l -> l
					.logoutUrl("/logout")
					.logoutRequestMatcher(new AntPathRequestMatcher("/logout", "GET"))
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

