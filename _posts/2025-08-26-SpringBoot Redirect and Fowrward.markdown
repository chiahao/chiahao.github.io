---
layout: post
title: "Spring Logout"
date: 2025-09-03 11:08:00
category: program
tags: [spring]
---


### 303/302 return
```java
@GetMapping("/login")
public String login2(HttpServletResponse resp) {
	String jwt = "123";
	Cookie cookie = new Cookie("JWT_TOKEN", jwt);
	cookie.setHttpOnly(true);
	cookie.setPath("/");
	resp.addCookie(cookie);

	return "forward:/index.html";
	// or 
	return "index.html";
}
```



```java
@GetMapping("/login")
public ModelAndView login(HttpServletResponse resp) {
	String jwt = "123";
	Cookie cookie = new Cookie("JWT_TOKEN", jwt);
	cookie.setHttpOnly(true);
	cookie.setPath("/");
	resp.addCookie(cookie);

	return new ModelAndView("redirect:index.html");
}
```

```java
@GetMapping("/login")
public ResponseEntity<Void> login(HttpServletRequest req, HttpServletResponse resp) {
	String jwt = "123";

	ResponseCookie cookie = ResponseCookie.from("JWT_TOKEN", jwt)
			.httpOnly(true)
			.secure(true)
			.sameSite("Lax")
			.path("/")
			.maxAge(60 * 60)
			.build();
	ResponseEntity<Void> build = ResponseEntity.status(HttpStatus.SEE_OTHER) // 303
			.header(HttpHeaders.SET_COOKIE, cookie.toString())
			.location(URI.create("index.html"))
			.build();
	return build;
}
```


### Inside Server redirect
Note! If the 

```java
@GetMapping("/login")
public RedirectView redirectView(HttpServletResponse resp) {
	String jwt = "123";
	Cookie cookie = new Cookie("JWT_TOKEN", jwt);
	cookie.setHttpOnly(true);
	cookie.setPath("/");
	resp.addCookie(cookie);

	return new RedirectView("index.html");
}
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

