---
layout: post
title: "RolesAllowed in Jersey3"
date: 2024-01-04 15:50:00
category: jersey3
tags: [jersey3]
---

Ref:  [Exception Handling With Jersey](https://www.baeldung.com/java-exception-handling-jersey)

```java
public class UnrecognizedPropertyExceptionMapper implements ExceptionMapper<UnrecognizedPropertyException> {
	@Override
	public Response toResponse(UnrecognizedPropertyException exception) {
		return Response.status(NOT_ACCEPTABLE)
				.entity("Parameter NOT acceptable.")
				.type(MediaType.APPLICATION_JSON)
				.build();
	}
}
```

```java
import jakarta.ws.rs.core.Feature;
import jakarta.ws.rs.core.FeatureContext;
import jakarta.ws.rs.ext.Provider;
import org.glassfish.jersey.server.filter.RolesAllowedDynamicFeature;

@Provider
public class ClassPathScanWorkAroundFeature implements Feature {
	@Override
	public boolean configure(FeatureContext featureContext) {
		featureContext.register(UnrecognizedPropertyExceptionMapper.class);
		return true;
	}
}
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


