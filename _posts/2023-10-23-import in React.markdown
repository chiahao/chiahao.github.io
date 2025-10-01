---
layout: post
title: "import in React"
date: 2023-10-23 10:18:00
category: react
tags: [react]
---

### Slow
**Named**  
```javascript
import { Delete } from '@mui/icons-material';
```

### Fast
**Default**  
```javascript
import Delete from '@mui/icons-material/Delete';
```

### But

[Allow default import of Formik](https://github.com/jaredpalmer/formik/issues/1849)  
> @MaffooBristol default exports are a pretty controversial topic, but I personally avoid them because they create the ability to incorrectly name variables. For example, you could write import React from 'formik'; and spend forever figuring out why React doesn't have a memo function.
> 
> From a maintenance perspective, in the future we might decide that v7 of Formik uses a new "NewFormik" container, and at that point we wouldn't be able to change the default export to use it due to backwards compatibility. At that point, the default would be the legacy component, and we'd get issue after issue about it. Plus, some people use withFormik, so they might say "instead you should export withFormik as default!"


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


