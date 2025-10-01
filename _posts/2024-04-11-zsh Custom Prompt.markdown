---
layout: post
title: "zsh Custom Prompt"
date: 2024-04-11 09:34:00
category: programming
tags: [zsh]
---

{% raw %}
```bash
export PS1='%(?:%{%}%1{➜%} :%{%}%1{➜%} ) %{%}%~%{%} $(git_prompt_info)'
```
{% endraw %}

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

