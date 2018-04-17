---
title: "React Redux List Timers"
slug: react-redux-list-timers
---

# List Timers

The list of timers will display all of the timers you have created. 
Each timer displayed in the list will display the name, time, and  
a button to start or stop that timer. 

## mapStateToProps

Create a new component: 'src/list-timers.js'. 

```JSX
import React, { Component } from 'react'
import { connect } from 'react-redux'
import { selectTimer } from './actions'

class ListTimers extends Component {
  constructor(props) {
    super(props)

  }

  render() {
    return (
      <div>
       {/* render timers here */}
      </div>
    )
  }
}

const mapStateToProps = (state) => {
  return { timers: state.timers }
}

const mapDispatchToProps = () => {
  return { selectTimer }
}

export default connect(mapStateToProps, mapDispatchToProps())(ListTimers)
```

This implementation doesn't render the timers. It does set up the basic 
elements required for container/component to interface with Redux. 

The array of timers and selectTimer action are passed to the component 
via props through the 'mapStateToProps' and 'mapDispatchToProps' functions. 

## Component Architecture 

The Component Architecture in React is very flexible. Use it to 
your advantage in all situations. Use it to: 

Break pieces of larger components into smaller subcomponents. Using 
mulitple components makes each component smaller and easier to 
understand. 

Make components from elements that will be re-used in different contexts. 
Breaking things into more smaller components allows those components to 
be re-used. 

Use Components to create logical organization. Breaking elements into 
components gives your work a greater level of organization. 

Use components to offload display logic. Use components to handle 
tedious display logic like conversion of dates and times. 

### The Timer list

The timer list could be implemented as a single component. This
simple approach works but doesn't use React's Component 
architecture to your advantage. 

```JSX
render() {
    return (
      <div>
        {this.props.timers.map((timer, i) => {
          return (
            <div>
              <h2>{timer.name}</h2>
              <h1>{timer.time}</h1>
              <button>Start</button>
            </div>
          )
        })}
      </div>
    )
  }
```

Here the render method maps `this.props.timers` to: 

```JSX
<div>
  <h2>{timer.name}</h2>
  <h1>{timer.time}</h1>
  <button>Start</button>
</div>
```

This is simple but to make it completely functional you will have to 
add styles, possibly some more markup, the time will need to be formatted, 
and the button will require some logic and a click handler. 

With these required additions this component would bloat and become 
far less managable. In addition there would be a lot of logic, like 
formatting time, that is not core goal of this component, which is 
displaying a list of timers. 

## Timer View Component

A better approach is to create a component that is responsible for displaying 
a single timer. 

Create a file: 'src/timer-view.js'

```JSX
import React, { Component } from 'react'
import { connect } from 'react-redux'

import { toggleTimer } from './actions'

class TimerView extends Component {
  constructor(props) {
    super(props)

  }

  render() {
    return (
      <div>
        <h2>{this.props.timer.name}</h2>
        <h1>{this.props.timer.time}</h1>
        <button>Start</button>
      </div>
    )
  }
}

const mapStateToProps = (state) => {
  return {}
}

const mapDispatchToProps = () => {
  return { toggleTimer }
}

export default connect(mapStateToProps, mapDispatchToProps())(TimerView)
```

From here the render method in 'ListTimers' can be simplified to 

```JSX
render() {
  return (
    <div>
      {this.props.timers.map((timer, i) => <TimerView key={i} timer={timer} />)}
    </div>
  )
}
```

Notice: 'TimerView' takes a 'Timer' object as a prop: `timer={timer}`. The name 
and time properties are accessed as: `this.props.timer.name` and 
`this.props.timer.time` within 'TimerView'. 

You will need to import 'TimerView' at the top of 'ListTimers'

`import TimerView from './timer-view'`

## Challenges 



## Resources 

- 



