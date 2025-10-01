---
layout: post
title: "RESTful ConstraintViolationMapper"
date: 2025-09-19 08:58:00
category: program
tags: [jersey, java]
---




```java
public class ConstraintViolationMapper implements ExceptionMapper<ConstraintViolationException> {

	@Override
	public Response toResponse(ConstraintViolationException exception) {
		// Extract constraint violations
		Set<ConstraintViolation<?>> violations = exception.getConstraintViolations();

		// Construct error messages
		List<String> messages = new ArrayList<>();
		for (ConstraintViolation<?> violation : violations) {
			messages.add(violation.getMessage());
		}

		// Construct custom error response
		return Response.status(Response.Status.BAD_REQUEST)
				.entity(new RestErrorResponse(String.join(",", messages)))
				.type(MediaType.APPLICATION_JSON)
				.build();
	}
}
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

