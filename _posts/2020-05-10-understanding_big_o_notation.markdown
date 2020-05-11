---
layout: post
title:      "Understanding Big O Notation"
date:       2020-05-10 18:35:11 -0400
permalink:  understanding_big_o_notation
---


Since graduating from Flatiron’s software engineering course I’ve wanted to delve deeper into algorithms and data structures. When starting on this, I was quickly confronted with the idea of Big O notation, and specifically how this can impact the overall performance of the algorithms that I’m using in my program. 

O(1) describes an algorithm that will always execute in the same time (or space) regardless of the size of the input data set.

```
const func = ( resturaunts ) => {
    return 1 + 4
}
```

O(N) describes an algorithm that performance scales linearly, and so as the size of the input grows so does the amount of work that needs to be done. A good example of this is a function that creates a loop to iterate over each input value and check the value against a test. As the input grows, so does the size of the loop by the same amount as the function needs to check each value.

O(N2) represents an algorithm that performance is exponential to the input it’s given. This means that as the input grows, so does the runtime of the algorithm by a square of the input size. This is a common occurrence in problems where values in an input have the checked against other values in the same input. A brute force solution to these types of problems is to create a nested loop, whereby for each value of input, a sub loop is created to test all of the other values against it.

With a lot of the more complex algorithm problems I’ve come across, there’s usually a variety of solutions - some better than others. In my experience i’ve found some of the biggest improvements of algorithm runtime are made when a brute force solution, or most obvious solution is moved from O(N2) to O(N) with a single pass strategy, eliminating the need for a nested loop altogether through the use of maps to store the information during the initial pass. However such solution usually increases the space complexity of the solution, as new data structures that are tied to the size of the input are also being created. More often than not, the slight increase in runtime complexity is often outweighed by the benefits of using a single pass strategy. With all solutions though it is a balancing act, where the benefits of each solution have to considered before deciding the best strategy to take when coding an optimal solution. Understanding the BigO notation has greatly helped me identify the types of problems and therefore what possible solutions I have at my disposal.

