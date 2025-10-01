---
layout: post
title: "Spring Redirect and Fowrward"
date: 2025-09-05 08:58:00
category: program
tags: [spring, java]
---


# Not Sure Work Or Not

```java
@Component
public class LdapAuthProvider implements AuthenticationProvider {

	private final ObjectProvider<HttpServletRequest> requestProvider;

	public LdapAuthProvider(ObjectProvider<HttpServletRequest> requestProvider) {
		this.requestProvider = requestProvider;
	}

	@Override
	public Authentication authenticate(Authentication authentication) throws AuthenticationException {

		HttpServletRequest request = requestProvider.getIfAvailable();
		var login_id = ntnu.auth.Auth.loginByLDAPWebService(requestProvider.getObject());
		login_id = "chiahao";
		if (login_id == null || login_id.isEmpty()) {
			throw new BadCredentialsException("Invalid credentials");
		}

		// 認証成功トークンを返す（資格情報は null にしても良い）
		return new UsernamePasswordAuthenticationToken(login_id, null, new ArrayList<>());
	}

	@Override
	public boolean supports(Class<?> auth) {
		return UsernamePasswordAuthenticationToken.class.isAssignableFrom(auth);
	}
}
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

