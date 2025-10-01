---
layout: post
title: "Gzip Fail Preview"
date: 2024-08-05 15:00:00
category: programming
tags: [swift]
---

```xml
linker command failed with exit code 1
Showing Recent Messages
Undefined symbol: (extension in Gzip):Foundation.Data.gunzipped() throws -> Foundation.Data
Showing Recent Messages
Undefined symbol: (extension in Gzip):Foundation.Data.isGzipped.getter : Swift.Bool
```

Add Gzip in `Build Phases` -> `Link Binary With Libraries`.

NOTE! not `Target Dependencies`



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

