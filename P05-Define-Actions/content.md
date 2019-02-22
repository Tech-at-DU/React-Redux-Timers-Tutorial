---
title: "React Redux Timers - Defining Actions"
slug: react-redux-timers-defining-actions
---

## Defining Actions

The Flux pattern and Redux require that
you define **actions** that describe how data can be modified. A few key points around actions:

1. **Data can only be modified through actions.**
1. Each action should be defined as a `const` with string value.
1. Each action needs an **action creatoer**

But wait, we just covered actoins, what's an action creator? An action creator is a _function that returns an object with a **type**, and a **payload** when a value needs to accompany the action._

For example, a `SELECT_BOOK` action creator might look like this:

```js
export const selectBook = (index) => {
  return {
    type: SELECT_BOOK,
    payload: { index }
  }
}
```

# Timer Actions

Let's start by defining the actions before making the app!

The app needs to do the following things with timers:

- Add a new timer
- Reset a timer
- Delete a timer
- Start a timer
- Stop a timer
- Toggle a timer
- Select a timer

First we need a place to store all these actions:

> [action]
>
> Create the folder `src/actions`, and then add this file: `src/actions/index.js`.

All actions are going to be defined within `src/actions/index.js`.

Let's build each of these out, action by action:

# Add Timer

`ADD_TIMER` - Creating a timer will add a new timer object to an array of timer objects held by the store.

> [action]
>
> Add the following to `src/actions/index.js`:
>
```js
export const addTimer = (name) => {
  return {
    type: NEW_TIMER,
    payload: { name }
  }
}
```

# Reset Timer

`RESET_TIMER` - Sets the time of a timer to 0. This requires the id or index of a timer.

> [action]
>
> Add the following to `src/actions/index.js`:
>
```js
export const resetTimer = (index) => {
  return {
    type: RESET_TIMER,
    payload: { index }
  }
}
```

# Delete Timer

`DELETE_TIMER` - Removes a timer from the array of timers in the
store. This will require the index of the timer.

> [action]
>
> Add the following to `src/actions/index.js`:
>
```js
export const deleteTimer = (index) => {
  return {
    type: DELETE_TIMER,
    payload: { index }
  }
}
```

# Start Timer

`START_TIMER` - This action starts a timer running, and
requires the index of the timer to start.

> [action]
>
> Add the following to `src/actions/index.js`:
>
```js
export const startTimer = (index) => {
  return {
    type: START_TIMER,
    payload: { index }
  }
}
```

# Stop Timer

`STOP_TIMER` - Stops a timer at the current time. This requires
the index of the timer.

> [action]
>
> Add the following to `src/actions/index.js`:
>
```js
export const stopTimer = (index) => {
  return {
    type: STOP_TIMER,
    payload: { index }
  }
}
```

# Toggle Timer

`TOGGLE_TIMER` - Starts or stops a timer. This requires the
index of the timer.


> [action]
>
> Add the following to `src/actions/index.js`:
>
```js
export const toggleTimer = (index) => {
  return {
    type: TOGGLE_TIMER,
    payload: { index }
  }
}
```

# Select Timer

`SELECT_TIMER` - Selects a timer. Selecting a timer will
display details about that timer. This requires the index
of the timer.

> [action]
>
> Add the following to `src/actions/index.js`:
>
```js
export const selectTimer = (index) => {
  return {
    type: SELECT_TIMER,
    payload: { index }
  }
}
```

# Did We Forget Something?

Alright, all of our actions are in place, and we're exporting our action creators! We're still missing one last piece though: in order for other modules to access these actions, _we need to export our actions as well!_

> [action]
>
> Add the following export lines to the top of `src/actions/index.js`:
>
```js
export const NEW_TIMER    = "NEW_TIMER"
export const RESET_TIMER  = "RESET_TIMER"
export const DELETE_TIMER = "DELETE_TIMER"
export const START_TIMER  = "START_TIMER"
export const STOP_TIMER   = "STOP_TIMER"
export const TOGGLE_TIMER = "TOGGLE_TIMER"
export const SELECT_TIMER = "SELECT_TIMER"
...
```

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'added Timer actions'
$ git push
```
