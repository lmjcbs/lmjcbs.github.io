---
layout: post
title:      "Common errors to watch out for in Javascript"
date:       2020-06-17 21:25:38 +0000
permalink:  common_errors_to_watch_out_for_in_javascript
---


In this blog post I'll be looking at some of the more common gotchas to watch out for when working with javascript. This list is intended to be a point of reference and will be expanded as I come across new quirks in the future.

### var vs let keywords

the var and let keywords are both used to assign variables in javascript however they have slight nuances in how they behave, consider the following example.

```
// using let
for(let i=0; i<5; i++) {
  //...
}
console.log(i) // Reference Error: i is not defined

// using var
for(var j=0; j<5; j++) {
  //...
}
console.log(j) // 5
```

This behaviour happens because `let` is block scoped to the `for` loop and therefore the `console.log` has no way to find the value of `i`, whereas the `var` keyword can be hoisted outside of the scope it is called in.

### Truthy vs falsy and deep equality

In javascript `==` checks for whether a value is truthy or falsy and then compares them. That's why it's possible to have results such as 
```
0 == false   // true
```
crop up in your code, this can be explained because JavaScript sees `0` as a falsy value, as well as `false`, which is also a falsy value.

Using Javascript's deep comparison triple equals comparator we can extend the check to types, which usally gives the desired result of false.

```
0 === false   // false
```
