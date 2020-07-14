---
layout: post
title:      "Cleaning up with React hooks "
date:       2020-03-19 13:37:42 -0400
permalink:  cleaning_up_with_react_hooks
---


With the release of React 16.0 came hooks, which are functions that let us hook into the React state and lifecycle features from function components and are an **alternative** method to handle component state and lifecycle methods. In this post, I'll be taking a deeper dive into how to make the switch to hooks in the context of my React project design vault.

Throughout my project I made use of input fields to allow users to interact with my application, modifying the data they saw as well as submitting their own data. Regardless of the intended functionality behind the input the react components all contained a similar boilerplate of code to store the value in component state and update the input field value from component state.


```javascript
import React, { Component } from 'react'

class CustomForm extends Component {
  state = {
    name: ''"
  }

  handleOnChange = (event) => {
    this.setState({
      name: event.target.value
    })
  }

  handleOnSubmit = (event) => {
    event.preventDefault();
		postNameValueToApi(this.state.name)
    this.setState({
      name: ''"
    })
  }

  render() {
    return(
      <div>
        <form onSubmit={this.handleOnSubmit}>
          <input type='text' value={this.state.name} name='name' onChange={(event) => this.handleOnChange(event)}></input>
          <input type='submit'/>
        </form>
      </div>
    )
  }
}

export default CustomForm
```

Here we have a customForm component that takes user input and upon submitting the form, calls our postNameValueToApi function from within the handleOnSubmit. Although functioning correctly, there's a lot of boilerplate code within the component, such as setting the component state, as well as the handleOnChange and handleOnSubmit functions that are passed to the input tag inside our render function.

Hooks allow us to extract this core functionality into a single hook outside of the component to be called upon as and when required. To implement this, we need to extract the input field behaviour outlined above.

```javascript
import { useState } from 'react';

export const useFormInput = (initialValue) => {
  const [value, setValue] = useState(initialValue);

  const handleChange = (e) => {
    setValue(e.target.value);
  };

  return {
    value,
    onChange: handleChange
  };
};
```

Firstly we import useState from the React library. With useState, we can pass an initial value as the argument and assign that to two variables, in this example `value` and `setValue` to retrieve the current value and set the value to a new value. Similarly to our react component, we have a handleChange function that updates the value we stored in the components state by pulling the `e.target.value` from our input tag. Instead of using `setState` to modify a key-value pair in the state object, we use setValue to directly update `value`. Lastly, we are returning an object that contains the value and a key-value pair that holds a reference to the handleChange function we defined earlier.

Great, our custom form input hook is created, how do we now use this in our previous class component example?

First, we need to import our custom exported hook from where we chose to store it. For reusable hooks, I like to organise them into their own folder inside utils that can be used across the React application.

```javascript
import React, { Component } from 'react'
import useFormInput from '../../utils/hooks/useFormInput'

class CustomForm extends Component {

  const name = useFormInput('') 

  handleOnSubmit = (event) => {
    event.preventDefault();
		postNameValueToApi(name.value)
  }

  render() {
    return(
      <div>
        <form onSubmit={this.handleOnSubmit}>
          <input type='text' name='name' { ...name }></input>
          <input type='submit'/>
        </form>
      </div>
    )
  }
}

export default CustomForm
```

Here we've made a few key changes to our component

*  imported the hook at the top of our component file

*  we defined our name variable to the return value of our hook, setting the initial value to an empty string, as we did previously in setState in our previous example.

* destructed our name object, sets both the value and onChange attributes of our input tag, as we defined it in the return value of our custom hook.

And with these changes, we now have a simple form component that's much leaner after removing the typical lifecycle method boilerplate that's required for common input handling in React. Furthermore we also now have a reusable hook that makes use of useState ready to use for the next time we want to handle form input.







