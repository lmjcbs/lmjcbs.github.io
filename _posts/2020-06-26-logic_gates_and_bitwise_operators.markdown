---
layout: post
title:      "Logic gates and bitwise operators"
date:       2020-06-26 06:31:10 +0000
permalink:  logic_gates_and_bitwise_operators
---



In this blog post i'm going to firstly be taking a look at logic gates and the principles behind how they work and then how this can be translated and utilised in JavaScript.

Three of the most common logic operators are the AND, OR and NOT.

The AND gate
* Takes two inputs and only outputs a signal if **both** inputs contain a signal.

The OR gate
* Takes two inputs and outputs a signal if either or / both of the inputs contain a signal. This can be summarised as, if any of the inputs contain a signal, an output will be produced.

The NOT gate
* Takes a single input and always outputs the inverse of the input signal.

These three gates are respresented in JavaScript using the `&& || !` operators respectively. Here are some example use cases

AND `true && false = false`, as both inputs for an AND gate need to have a signal, or in the case of JavaScript a truthy value, in this case a `true` boolean value.

OR `true || false = true`, as the conditions are met to satisfy the OR gate. At least one of the inputs contains a `true` value.

NOT `!true = false`, here the sole input signal is simply inversed, so our true input is converted to a false value.

These come in extremely useful for controlling the flow of applications to trigger certain effects, only once certain conditions are met.
