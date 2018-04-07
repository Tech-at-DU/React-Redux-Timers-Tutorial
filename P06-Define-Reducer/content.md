---
title: "React Redux Define Reducer"
slug: react-redux-define-reducer
---

# Define Reducer

Next you need a reducer to handle chnages in state. As a first step it 
would be good to get an idea of what application state will look like.

Remember the store is a JavaScript Object with key values that 
represent 'pieces' of state. A piece of state is one Key on the 
Object that holds one part of state. 

For this app we will put an array of timers on one piece of state, 
and the index of the selected timer on another piece of state. 

With this arrangement the store would look like this: 

```JavaScript
{
  timers: [ timer1, timer2, timer3, ...],
  selectedTimer: 0
}
```

Timer will be generated from the Timer class and will look like this: 

```JavaScript
{
  name: "Test", 
  time: 17872,
  isRunning: false
}
```

You will need to define two reducers one for 'timers' and the other 
for 'selectedTimer'. 

**Selected Timer Reducer**

The selectedTimer Reducer will need to set the selectedTimer to the 
value passed in the payload of the Select Timer action. Since this 
is a Number/Primitive type you can just return the new value. 

Primitives like Numbers, Strings, and Booleans are value types. 
When you set the value of a variable containing one of these types
you are creating a new value and replacing the old value. 

**Timers reducer**

In the case of the Timers Reducer you will have more work to do. 
The timers reducer is responsible for managing the array of Timer
objects. 

Arrays are not primitives instead these passed as references. 
When you make changes to an Array you are updating the values stored 
at a location in memory. In this case the reference stays even 
though the value stored there may have changed. 

**Redux requires a reducer to return a new object.** If a reducer 
returns the same object Redux will not see a change and will not 
update. 

## Challenges 

Create a folder 'src/reducers', then add a file 'src/reducers/index.js'. 
This file will "combine" the reducers and export them. Before you can 
combine the reducers you will need to create some reducers!

Create a new file: 'src/reducers/select-timer-reducer.js'. 

Define a reducer here to manage the selected timer. 

```JavaScript 
import { SELECT_TIMER } from '../actions'

const selectTimerReducer = (state = null, action) => {
  switch (action.type) {
    case SELECT_TIMER:
      // Return the index of the new timer

    default:
      return state
  }
}

export default selectTimerReducer
```


Define a reducer for timers. Create a new file: 'src/reducers/timers-reducer.js'.

A reducer is a function that takes in state, and an action as parameters and 
returns state. The reducer should always return a new copy of state. It should 
never modify state. In the case of the timers-reducer the value stored is an 
array. For any changes to timers this reducer must create a copy of the array
and return that. 

```JavaScript
import { NEW_TIMER, RESET_TIMER, DELETE_TIMER, START_TIMER, STOP_TIMER, TOGGLE_TIMER } from '../actions';

const timerReducer = (state = [], action) => {
  switch (action.type) {
    case NEW_TIMER:
      // Add a new timer, return a copy of state

    case RESET_TIMER:
      // Reset the timer at index, return a copy of state

    case DELETE_TIMER:
      // Remove the timer at index, return a copy of state. 

    case START_TIMER:
      // Set the isRunning property of the timer at index to true, return a copy of state

    case STOP_TIMER:
      // Set the isRunning property of the timer at index to false, return a copy of state

    case TOGGLE_TIMER:
      // Invert the isRunning property of timer at index, return a copy of state

    default:
      return state;
  }
}

export default timerReducer;
```

Combine your reducers in 'src/reducers/index.js'.

```JavaScript
import { combineReducers } from 'redux';

import timerReducer from './timers-reducer';
import selectTimerReducer from './select-timer-reducer';

export default combineReducers({
  timers: timerReducer,              // array
  selectedTimer: selectTimerReducer, // int/number
});
```

Last define the Provider component. Make this the top level
component in App.js. Remember to store as a prop. 
Your App Component should look something like this. 

```JSX
class App extends Component {
  render() {
    return (
      <Provider store={store}>
        <div className="App">
          <header className="App-header">
            <h1 className="App-title">Welcome to React</h1>
          </header>
          <p className="App-intro">
            Tmrz
          </p>
        </div>
      </Provider>
    );
  }
}
```

At this stage the app is all set up to use redux! You can build 
components that use connect to the store and send actions. 

## Resources 

- 



