---
layout: post
title: "Auto Compile SCSS IN Intellij IDEA"
date: 2022-03-02 09:46:00
category: programming
tags: [idea]
---

1. Install plugin: `File Watchers`

2. 裝好了才會在 Setting -> Tools 裡面看到 File Watchers

3. 直接按 `Command + N` 新增（新版的 IDEA 沒有看到對應的 template）

4. 重點是 Argument:  
`$FileDir$/$FileName$:$FileDir$/../css/$FileNameWithoutExtension$.css --style compressed`
or  
`$FileDir$/$FileName$:$FileDir$/../css/$FileNameWithoutExtension$.css --style compressed --load-path=$ProjectFileDir$/node_modules`  

如果指定了 load-path, 就不用再: 
`@import "../../node_modules/bootstrap/scss/functions";`  
而只要寫:  
`@import "bootstrap/scss/functions";`  


5. Output paths to refresh 裡輸入:
`$FileNameWithoutExtension$.css:$FileNameWithoutExtension$.css.map`

6. 把「Working Directory and Environment Variables」展開,  
在「Woring Directory」裡輸入:
`$FileDir$`


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

