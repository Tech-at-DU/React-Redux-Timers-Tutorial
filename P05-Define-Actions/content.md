---
title: "React Redux Timers - Defining Actions"
slug: react-redux-timers-defining-actions
---

# Defining Actions

The Flux pattern and Redux require that
you define actions that describe how data can be modified.

**Data can only be modified through actions.**

For this project you will start by defining the actions before
making the app!

The app needs to do the following things.

- Create a new timer
- Reset a timer
- Delete a timer
- Start a timer
- Stop a timer
- Toggle a timer
- Select a timer

**ADD_TIMER** - Creating a timer will add a new timer
object to an array of timer objects held by the store.

**RESET_TIMER** - Sets the time of a timer to 0. This requires
the id or index of a timer.

**DELETE_TIMER** - Removes a timer from the array of timers in the
store. This will require the index of the timer.

**START_TIMER** - This action starts a timer running, and
requires the index of the timer to start.

**STOP_TIMER** - Stops a timer at the current time. This requires
the index of the timer.

**TOGGLE_TIMER** - Starts or stops a timer. This requires the
index of the timer.

**SELECT_TIMER** - Selects a timer. Selecting a timer will
display details about that timer. This requires the index
of the timer.

Each action should be defined as a `const` with string value.  

**Defining action Creators**

You will also need to define some action creators. One for each
action. An action creator is a function that returns an object
with a type, and a payload when a value needs to accompany the
action.

For example the SELECT_TIMER action creator might look like this:

```
export const selectTimer = (index) => {
  return {
    type: SELECT_TIMER,
    payload: { index }
  }
}
```



## Challenges

Create folder: 'src/actions', and then add file: 'src/actions/index.js'.

Define all of the actions above in 'src/actions/index.js'

Add an action creator for each action type in 'src/actions/index.js'

Be sure to export each action and each action creator. You will need
access to these in other modules.

## Resources

-
