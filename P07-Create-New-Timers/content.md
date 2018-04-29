---
title: "React Redux Timers - Create new Timers"
slug: react-redux-timers-create-new-timers
---

# Create new Timers

So far you have been working on getting Redux and React up and 
running and no work has gone into components. Now it's time to 
get the components working. 

With actions and reducers in place you can now create 
containers/components that display state from the store and 
send actions to update the store. 

## Show a list of timers

You need to create two components. 

**Displaying Components**

The Timer display can be as simple as a div with the name, 
time, and start/stop button. 

**New Timer Component**

The new timer component should have field (controlled component)
to input a name and a button to save the timer. 

Start with the new Timer Component. Keep in mind that we 
won't see timers until the Timer list component is created. 

## Challenges 

**New Timer Component/Container**

Create a component with an input and a button. This component 
shuold use the controlled conponent pattern.

Use 'mapDispatchToProps' to connect the 'newTimer'
action creator to this component. Here is a stub for the 
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



