---
layout: post
title:      "Common errors to watch out for in Javascript"
date:       2020-06-17 17:25:39 -0400
permalink:  common_errors_to_watch_out_for_in_javascript
---


In this blog post I'll be looking at some of the more common gotchas to watch out for when working with javascript. This list is intended to be a point of reference and will be expanded as I come across new quirks in the future.

### Assinging values to variables

consider the following example;

```
let array1 = [1,2,3];
let array2 = array1;
array2.push(4);
array2; // [1,2,3,4]
array1; // [1,2,3,4] // Also has 4 appended to it.
```

The key gotcha here is that primitive values (number, boolean, string, undefined, symbol, null) are assigned by copying the value to a new space in memory, while object values (arrays, functions, dates) are assigned by reference, meaning that objects will not be cloned from one variable to another, but instead the variable acts as a reference to the object.

In our example here `array1` and `array2` are both references to the same array in memory, and so appending 4 to the array that both `array1` and `array2` are referencing causes the change to appear in both places.

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

### Semi colon injection

JavaScript is typically very lenient about the use of semi colon's in that it will automatically inject semi colons where needed at runtime, in the case they have been omitted. This has the advantage of not having to worry about every single semicolon, in order to avoid errors at runtime.

```
let i = 0 // will be read as let i = 0; 
```

similarly spacing your code on to multiple lines will cause unwanted errors as JavaScript inserts semicolons where it sees fit.

```
function add(x, y) {
  return
  x+y
}
```

this example will not return x+y as a semicolon is inserted after `return`. The above code is interpreted as follow;

```
function add(x, y) {
  return;
  x+y; // this is never read
}
```

In order to avoid the above behaviour you can make use of parentheses for grouped expressions or multi-line expressions.

```
function add(x, y) {
   return (
     x + y
   ); // will return a + b
}
```

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
