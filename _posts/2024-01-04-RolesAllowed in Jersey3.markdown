---
layout: post
title: "RolesAllowed in Jersey3"
date: 2024-01-04 15:50:00
category: jersey3
tags: [jersey3]
---

Ref:  [Jersey ResourceConfig doesn't auto discover but Application does?](https://stackoverflow.com/questions/45700344/jersey-resourceconfig-doesnt-auto-discover-but-application-does)

There are two ways to achieve:  
1. `Application` with `Feature`:  this would auto discover

```java
import jakarta.ws.rs.ApplicationPath;
import jakarta.ws.rs.core.Application;


@ApplicationPath("/api")
public class RestApplication extends Application {}
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
		featureContext.register(RolesAllowedDynamicFeature.class);
		return true;
	}
}
```

2. `ResourceConfig` won't auto discover, need to manually assign packages to scan

```java
import jakarta.ws.rs.ApplicationPath;
import org.glassfish.jersey.server.ResourceConfig;
import org.glassfish.jersey.server.filter.RolesAllowedDynamicFeature;

@ApplicationPath("/api")
public class RestApplication extends ResourceConfig {

	public RestApplication() {
		packages(
				"tw.rainbow.edu.personcheckin.manage.filter",
				"tw.rainbow.edu.personcheckin.manage.endpoint",
				"tw.rainbow.edu.personcheckin.manage.resource");
		register(RolesAllowedDynamicFeature.class);
	}
}
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


