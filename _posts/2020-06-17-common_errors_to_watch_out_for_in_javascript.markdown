---
layout: post
title:      "Common errors to watch out for in Javascript"
date:       2020-06-17 17:25:39 -0400
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

### Using import and export ES2015 syntax

`import` and `export` may only appear at the top-level, or outer most scope of the module file itself. Importing a specific function within a block for use will throw an error.

```
if (conditionIsTrue) {
  import { myFunc } from 'myModule'; // error: 'import' and 'export' may only appear at the top-level
  myFunc();
}
```

In order to fix this error, all import statements must be moved out of the if statement scope and into the outer module scope.

```
import { myFunc } from 'myModule';  // now exists at the top of the module.

if (conditionIsTrue) {
  myFunc(); // will no longer throw an error
}
```
