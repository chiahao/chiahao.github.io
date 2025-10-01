---
layout: post
title: "Spread Syntax"
date: 2022-03-04 08:23:00
category: javascript
tags: [javascript]
---

* Function argument list (`myFunction(a, ...iterableObj, b)`)
* Array literals (`[1, ...iterableObj, '4', 'five', 6]`)
* Object literals (`{...obj, key: 'value'}`)

### Replace apply()
```javascript
function myFunction(x, y, z) { }
let args = [0, 1, 2];
myFunction.apply(null, args);
```
can be written as
```javascript
function myFunction(x, y, z) { }
let args = [1, 2, 2];
myFunction(...args);
```
can be used multiple time.
```javascript
function myFunction(v, w, x, y, z) { }
let args = [0, 1];
myFunction(-1, ...args, 2, ...[3]);
```

### Apply for new operator
When calling a constructor with new it's not possible to directly use an array and apply() (apply() does a [[Call]] and not a [[Construct]]).  
However, an array can be easily used with new thanks to spread syntax:
```javascript
let dataFields = [1970, 0, 1]; // 1 Jan 1970
let d = new Date(...dataFields);
```

### Copy an array
```javascript
let arr = [1,2,3];
let arr2 = [...arr]; // like arr.slice()
```

```javascript
arr2.push(4);
// arr2 becomes [1,2,3,4]
// arr remains unaffected
```

### Maybe Unsuitable for copying multimenstional arrays  

Spread syntax effectively goes one level deep while copying an array.  
(The same is true with `Object.assign()`.)

```javascript
let a = [[1], [2], [3]];
let b = [...a];

b.shift().shift();
// 1

// Oh no!  Now array 'a' is affected as well:
a
// [[], [2], [3]]
```

### A better way to concatenate arrays
```javascript
let arr1 = [0, 1, 2];
let arr2 = [3, 4, 5];

// Append all items from arr2 onto arr1
arr1 = arr1.concat(arr2);

arr1 = [...arr1, ...arr2];
// Note: Not to use const otherwise, it will give TypeError (invalid assignment)
```

`Array.propotype.unshift()` is often used to insert an array of values at the start of an existing array.
```javascript
// Prepen all items from arr2 onto arr1
Array.prototype.unshift.apply(arr1, arr2);
// arr1 is now [3, 4, 5, 0, 1, 2]

arr1 = [...arr2, ...arr1]
```
**Unlike** `unshift()`, this creates a new `arr1`, and does not modify the original `arr1` array in-place.


### Spread in object literals
> The [Rest/Spread Properties for ECMAScript](https://github.com/tc39/proposal-object-rest-spread) proposal (ES2018) added spread properties to [object literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#1). It copies own enumerable properties from a provided object onto a new object.
> Shallow-cloning (excluding prototype) or merging of objects is now possible using a shorter syntax than Object.assign().

```javascript
let obj1 = { foo: 'bar', x: 42 };
let obj2 = { foo: 'baz', y: 13 };

let cloneObj = { ...obj1 };
// Object { foo: "bar", x: 42 }

let cloneObj = { ...obj1, ...obj2 };
// Object { foo: "baz", x: 42, y: 13 }
```

Note that Object.assign() triggers setters, whereas spread syntax doesn't.

> Note that you cannot replace or mimic the `Object.assign()` function:  

```javascript
let obj1 = { foo: 'bar', x: 42 };
let obj2 = { foo: 'baz', y: 13 };
const merge = ( ...objects ) => ( { ...objects } );

let mergeObj1 = merge (obj1, obj2);
// Object { 0: { foo: 'bar', x: 42}, 1: { foo: 'baz', y: 13 } }
```

## Only for iterables
> Spread syntax (other than in the case of spread properties) can only be applied to iterable objects like Array, 
> or with iterating functions such as `map()`, `reduce()`, and `assign()`.
> Many objects are not iterable, including `Object`:
```javascript
let obj = {'key1': 'value1'};
let array = [...obj]; // TypeError: obj is not iterable
```
> To use spread syntax with these objects, you will need to provide an iterator function.



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


