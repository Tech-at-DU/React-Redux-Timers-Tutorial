# Persisting Timers

Your timers are working, they're styled and looking fly, but they still don't quite do one thing yet: persist! If you refresh the page, or open a new tab on `localhost`, the timers disappear.

In this last chapter, we'll fix that by persisting the timers with local storage.

# Overview

Before you begin, let's take inventory of a few things:

1. The Redux store is a JavaScript Object.
1. Local storage only allows for strings.
1. Therefore, _if we can convert the Redux store to JSON, it would be possible to convert the store to local storage and back._

JSON is JavaScript Object Notation. It's a string format that represents a JavasScript object. You can use it as a JS object in most cases and JS objects will convert to JSON most of the time. 

When does it not work? If you're Object contains values that things other than: Strings, Numbers, Arrays, or Objects. What else is left? functions and classes! An Object that contains a function can't be converted to JSON. 

# Save and Retrieve the store

First step is to define a key to be used with local storage. Next we need to define two methods to load and save state from local storage.

Since it's not related to a a specific component, action, or reducer, our `utils` folder feels like a good place to put this.

Add the following to the top of the `/src/utils/persistState.js` file:

```js
const TMRZ_STATE = "TMRZ_STATE"

// Load State
export const loadState = () => {
  try {
  // Grab the state from local storage
    const serializedState = localStorage.getItem(TMRZ_STATE)
    if (serializedState === null) {
      return undefined
    }
    // convert the string into JSON for the Redux store
    return JSON.parse(serializedState)
  } catch(err) {
    return undefined
  }
}

// Save State
export const saveState = (state) => {
  try {
    // convert the state from JSON, into a string
    const serializedState = JSON.stringify(state)
    // save the state to local storage
    localStorage.setItem(TMRZ_STATE, serializedState)
  } catch(err) {
    console.log("Error saving data")
  }
}

```

To persist state subscribe to changes from the `store` in `src/app/app.js`. Import the functions you added to `utils.persistState.js`:

```js
...
import { loadState, saveState } from '../utils/persistState'
...
```

Modify this block where you configured your store. Here you are loading your persisted store from local storage when the app launches. 

```js
export const store = configureStore({
  reducer: {
		timers: timersReducer
	},
	preloadedState: loadState() // 5
})
```

Now add this new block.

```js
store.subscribe(() => {
	saveState(store.getState());
})
```

This block defines a a callback that will be called when the store is updated. When a change is made to the store the callback function gets the current app state and saves it to local stoage. 

# Needs More Throttle

In this arrangement `saveState()` is being called each time the store changes. Since the timers update the store every 50ms, this could cause performance issues if we're writing to local storage every 50ms as well. We can solve this with a **throttling method**. This is a method that limits the calls to other methods over time.

It might be possible to improve performance by throttling calls to `saveState()`. [Lodash](https://lodash.com/) has a throttle method we can use to help us out.

Install Lodash via npm:

```bash
$ npm i --save lodash
```

Lodash has many methods. By default we will get the whole library, but let's just import only the part that we need, in this case `throttle`.

import lodash's throttle method into `App.js`

```js
import throttle from 'lodash/throttle'
```

Finally, let's tell our store to save state every 1000ms using Lodash's throttle method. Replace the current `store.subscribe` call with the following in `App.js`:

```js
store.subscribe(throttle(() => {
  saveState(store.getState())
}, 1000));
```

Now the timers are updating every 50ms, but state is only being written to local store every 1000ms.

Try refreshing the tab or opening a new tab on `localhost` and see your timers persist!

Congrats! We got some practice managing local storage in the context of **managing application state through the Flux pattern!** Not to mention some pretty sweet timers to boot.

As you go through this FEW course, try to tie the concepts you learned here into the course material. The foundational work here on building React apps will be used to make bigger and bolder apps down the road!

## Technical Planning

1. ~~Review Project~~
2. ~~Create timer objects~~
3. ~~Setup Redux Toolkit~~
4. ~~Setup React Redux Provider~~
5. ~~Create New Timer Component~~
6. ~~Create List Timer Component~~
7. ~~Create Timer View Component~~
8. ~~Keeping Time~~
9. ~~Format Time~~
10. ~~Styling the App~~
11. **Persisting Timers**
12. Stretch Goals

# Now Commit

```bash
$ git add .
$ git commit -m 'persisting timers'
$ git push
```
