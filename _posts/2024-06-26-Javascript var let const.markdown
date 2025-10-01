---
layout: post
title: "Javascript var let const"
date: 2024-06-26 08:32:00
category: programming
tags: [javascript]
---

#### Ref.: [Var, Let, and Const – What's the Difference?](https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/)

# var is globally scoped or function scoped.

# var can be re-declared

# Hoisting of var
> They are all hoisted to the top of their scope.

```javascript
console.log (greeter);
var greeter = "say hello"
```

interpreted as:

```javascript
var greeter;
console.log (greeter);
greeter = "say hello"
```


# var
```javascript
var greeter = "hey hi";
var times = 4;

if (time > 3) {
  var greeter = "say Hello instead";
}

console.log(greeter); // "say Hello instead"
```

> While this is not a problem if you knowingly want greeter to be redefined, it becomes a problem when you do not realize that a variable greeter has already been defined before.


# let and const are block scoped

# let and const cannot be updated

# Hoisting of let

> Unlike `var` initialized as `undefined`, the `let` keyword is not initialized.
You'll get a `Reference Error` before declaration.


# const cannot be updated



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

