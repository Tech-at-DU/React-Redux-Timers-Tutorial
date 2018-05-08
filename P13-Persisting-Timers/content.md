---
title: "React Redux Timers - Persisting Timers"
slug: react-redux-timers-persisting-timers
---

In this sections the goal is to persist the timers with 
local storage.

# Overview

The Redux store is a JavaScript Object. Localstaorage only 
allows for strings. By converting the store to JSON it is
possible to convert the store to localStorage and back. 

Since the timers update the store often this could cause
performance issues. You can solve this with a throttling 
method. This is a method that limits the calls to other
methods over time. 

## Save and Retrieve the store

Define a key to be used with local storage. You can put 
this in 'App.js' or another file and import.  

`const TMRZ_STATE = "TMRZ_STATE"`

Next define two methods to load and save state from 
localstorage. 

```JS
// Load State
export const loadState = () => {
  try {
    const serializedState = localStorage.getItem(TMRZ_STATE)
    if (serializedState === null) {
      return undefined
    }
    return JSON.parse(serializedState)
  } catch(err) {
    return undefined
  }
}

// Save State
export const saveState = (state) => {
  try {
    const serializedState = JSON.stringify(state)
    localStorage.setItem(TMRZ_STATE, serializedState)
  } catch(err) {
    console.log("Error saving data")
  }
}
```

To persist state subscribe to changes from the store. 

```js
const persistedState = loadState()
const store = createStore(reducers, persistedState)
store.subscribe(() => {
  saveState(store.getState())
})
```

In this arrangement `saveState()` is being called each 
time the store changes. That's every time there is an 
action sent to the dispatcher/reducer. In the example 
code that was every 50 milliseconds. This might be too 
often for good performance.

It might be possible to improve perforance by throttling
calls to `saveState()`. Lodash has a throttle method. 

Import Lodash. 

`npm install --save lodash`

Lodash has many methods. By default you will get the 
whole library, you can also import only part that you 
need, in this case `throttle`. 

`import throttle from 'lodash/throttle'`

Modify the call to `store.subscribe()`:

```js
store.subscribe(throttle(() => {
  saveState(store.getState())
}, 1000));
```

Now the timer is updating every 50ms but state is only 
being written to local store every 1000ms. 

## Challenges 



## Resources 

- 


