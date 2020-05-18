---
layout: post
title:      "Class vs Functional Components"
date:       2020-05-17 15:30:56 -0400
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

Previously it was thought best to use class components as container components that would encompass a lot of the component logic, enclosed inside react's lifecycle methods such as `componentDidMount()` and then functional components would be used to display the data. However that has changed with the release of React 16.8 and the news hooks API that allows developers to get the same react lifecycle methods as before, but now packaged up in a smaller (and in my opinion) cleaner format. 


