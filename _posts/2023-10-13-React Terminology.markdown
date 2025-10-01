---
layout: post
title: "React Terminology"
date: 2023-10-13 08:45:00
category: react
tags: [react]
---

1. Hook
Functions starting with `use` are called Hooks.

2. Effect
Some components need to synchronize with external systems.  
*Effects* let you run some code after rendering so that you can synchronize your component with some system outside of React.  
***Effect*** **let you specify side effects that are caused by rendering itself, rather than by a particular event.**  
**Don't rush to add Effects to your components.**  Keep in mind that Effects are typically used to "step out" of your React code and synchronize with some *external* system.  
Every time your component renders, React will update the screen and *then* run the code inside `useEffect`.  In other words, `useEffect` **"deplays" a piece of code from running until that render is reflected on the screen.**  



3. useRef
`useRef` is a **React Hook** that lets you reference a value that's not needed for rendering.

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


