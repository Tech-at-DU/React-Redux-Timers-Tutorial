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

## Copying Array vs modifying an Array

JavaScript has a few primitive, here are three types: String, Number, 
and Boolean. Primitives are always stored as values and when assigned
those values are copied. 

Objects, Arrays, and Function are not copied when assigned to variables. 
Instead a reference to the original is assigned. Understanding this 
important to understanding JavaScript and Redux. 

Take a look at this code sample. 

https://repl.it/@MitchellHudson/Array-equivalency

## References and Redux <- IMPORTANT

This is one of the most important concepts to understand about working
with Redux. 

tl;dr: Your reducers must return a new copy of state if state is an
Object or Array. 

Redux requires that reducers return a new value when state changes. If 
state is an Object or an Array you must return a new copy of that Object
or Array. If modifying a nested Object or Array you must create a copy 
rather than modify the exisiting element. 

Why? Redux needs to see that the object has been changed. Objects are 
passed by reference, modifying an object doesn't create a new reference. 

Try it for yourself in code [here](https://repl.it/@MitchellHudson/Array-equivalency). 

## Value vs Reference

Primitive types: String, Number, Boolean create a new value when assigned. 
The following should not be unexpected: 

```JavaScript
var a = 11;
var b = a;
b += 9;
console.log(a, b); // 11, 20
```

Objects on the other hand are refernces and do not  create a new 
reference when assigned. The following might not be expected: 

```JavaScript
var a = [11];
var b = a;
b.push(44)
console.log(a, a.length); // [11, 44] 2
console.log(b, b.length); // [11, 44] 2
// Both a and b reference the same object. 
console.log(a === b); // true
```

The last line is important. The equality operator when used with 
Objects compares references! In the example both `a` and `b` 
reference the same object so they are equal. 

Consider the following: 

```JavaScript
var a = [11];
var b = [11];

console.log(a === b); // false
```

In this case a and b refernce two different object each of which 
happen to store the same value. They are not equivalent! 

Redux must see a change in state. If state is an object and it 
has been modified Redux will not see it as a new Object unless
it has been returned as a reference to a new Object. 

## Arrays Mutating vs Copy

There are few ways to copy an array. Mutating methods modify 
the original and return the same reference. These methods 
should not be used in your reducers! 

**Array methods**

The following methods are mututing: 

- push
- unshift
- splice

The following return a new reference:

- slice
- map
- filter

You can also create a copy of an array with the spread operator: 

```JavaScript
var a = [1, 22, 333];
var b = [...a, 4444]; // Creates a new array -> [1, 22, 333, 4444]
```

Here are a few of things you might do with an array in Redux. 

**Add a new item **

Use the spread operator

```JavaScript
// Creates a new array 
var newState = [...state, newItem];
```

Use slice()

```JavaScript
// Creates a copy of state
var newState = state.slice();
newState.push(newItem);
```

**Insert a new item**

Inserts a new item at index. 

```JavaScript
// Creates a new array with the elements from state starting at 0 to index - 1
// inserts newItem at index. 
// inserts the items from state starting at index after newItem.
var newState = [...state.slice(0, index), newItem, ...state.slice(index)];
```

**Copy an object in an array**

Remember if you are modifying an object in an array you need to 
create a copy of that object! 

Imagine state is an array of Objects with name and count `{name:"", count:0}`. 
You want to increase count for the object at index. 

```JavaScript 
var newState = state.map((item, i) => {
  if (i === index) {
    // Returns a new object with the values of item, and overwrites count with new value
    return {...item, count: item.count + 1}; 
  }                          
  return item;
})
```



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

- https://redux.js.org/recipes/structuring-reducers/immutable-update-patterns



