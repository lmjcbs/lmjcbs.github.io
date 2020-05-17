---
layout: post
title:      "Class vs Functional Components"
date:       2020-05-17 19:30:55 +0000
permalink:  class_vs_functional_components
---


Having worked on a hanful of React projects now, some my own and others group based, I've noticed that codebases often consist of both class and functional components at the same time, as they both can fulfill most tasks associated with creating components, business login and most importantly rendering a component. That left me with the question of, should I be using one over the other and what are the main differences between them.

## Class Components
* Utilise the newer ES6 Class syntax and often Extend the Component class that is provided by React
* Can make use of lifecycle methods such as `componentDidMount()` provided by the React library.
* Often used to store component state, in particular state that is to be then passed down to further child components. In the react component tree this is called a Higher order Component that handles the business logic.

## Functional Components
* Are basic JavaScript functions
* Often fulfill the role of a presentational component in projects, where the business logic is firstly handled outside of the functional component inside of a Higher order Component and is passed down. This keeps functional components leaner as they only have to concern themselves with rendering the data.
* Cannot make use of lifecycle methods such as `componentDidMount()` provided by the React library.
* Must simply contain the component to be rendered inside of the function `return`.


