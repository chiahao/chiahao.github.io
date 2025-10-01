---
layout: post
title: "Auto Redeploy(Hot Swap) On Intellij IDEA"
date: 2022-03-02 09:46:00
category: programming
tags: [idea]
---

It's just not like NetBeans! You Can't hot swap when save file!
1. **Artifacts** choose `Web Application: Exploded`
2. **Server** configuration: [On 'Update' action:] choose `Update classes and resources`
3. manually `Command + F10` to update running application.  
It seems that only allow hot swap in `Debug` mode.  


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

