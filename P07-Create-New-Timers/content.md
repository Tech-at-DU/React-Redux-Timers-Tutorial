---
title: "React Redux Create new Timers"
slug: react-redux-create-new-timers
---

# Create new Timers

So far you have been working on getting Redux and React up and 
running and now work has gone into the app. Now it's time to 
get the app working. 

With actions and reducers in place you can now create 
containers/components that display state from the store and 
send actions to update the store. 

Create a component that displays a list of Timers. At this
stage it won't display anything, you will have to make 
a component that creates new timers before there is anything 
to display. 

**Displaying Components**

The Timer display can be as simple as a div with the name, 
time, and start/stop button. 

**New Timer Component**

The new timer component should have field (controlled component)
to input a name and a button to save the timer. 

## A closer look at Redux state 

Redux relies on changes to state. What constitutes a changes in state? 

[Object Equivalency](https://repl.it/@MitchellHudson/Object-Equivalence-setState)

## Challenges 

**New Timer Component/Container**

Create a component with an input and a button. This component 
shuold use the controlled conponent pattern to implement to 
connect the value in the input to state.

It should also use 'mapDispatchToProps' to connect the 'newTimer'
action creator with this component. Here is a stub for the 
component: 

```JSX
import React, { Component } from 'react'
import { connect } from 'react-redux'

import { addTimer } from './actions'

class NewTimer extends Component {
  constructor(props) {
    super(props)

    // Store the name of of input name below on state
    this.state = {}
  }

  render() {
    return (
      <div>
        {/* make this a controlled component */}
        <input type='text' name="name" />
        {/* The save button should addTimer from props and pass the name from state */}
        <button>Save</button>
      </div>
    )
  }
}

const mapStateToProps = (state) => {
  return {}
}

const mapDispatchToProps = () => {
  return { addTimer }
}

export default connect(mapStateToProps, mapDispatchToProps())(NewTimer)
```

You may need to modify the names given here to match the 
names you have used. 

## Resources 

- 



