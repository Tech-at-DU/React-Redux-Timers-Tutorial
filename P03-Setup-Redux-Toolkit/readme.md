# Setup Redux Toolkit

In this step you will setup Redux Toolkit. Along the way you'll create some folders to organize your code. 

You'll also create a file to manage a "slice" of your application state.

Application state is stored in the the "store". The store is an object with many keys. The data stores at each of these keys is a slice. This application will have a single slice "timers" that stores an array of the Timer objects you created in the last step. 

## Organize your code

Make a new folder: `src/features`

You'll store some helper files here. 

Create a new folder: `src/features/timers`.

This will store all of your timer related code in one place. 

Move `Timer.js` into: `src/features/timers`

Redux Toolkit organizes your application data in slices. You'll define each "slice" in a file. 

For this project you'll store a list of timers. This list will be the Timers Slice! 

Add a new file `src/features/timers/timersSlice.js`

Add the following code: 

```JS
import { createSlice } from '@reduxjs/toolkit'
import makeTimer from './Timer'

const initialState = {
  value: [] // 1.0
}

export const timersSlice = createSlice({
  name: 'timers', // 2.0
  initialState, // 1.1
  reducers: { // 3.0
    
  },
})

// Action creators are generated for each case reducer function
export const {  } = timersSlice.actions

export default timersSlice.reducer
```

What you are going to do is create an array of Timer objects that is managed by Redux. You will be able to add new timers to the list, start and stop timers in the list, and delete timers from the list. 

This "slice" that you have defined here will be responsible for managing these things. 

`initialState` defines the value stored as an empty array. (1.0, 1.1)

The name of this "slice" of state is "timers". (2.0)

Reducers are how state is modified. Currently your reducers are empty. (3.0)

Add two actions to the reducer: 

```JS
... 

export const timersSlice = createSlice({
  name: 'timers',
  initialState,
  reducers: {

    addTimer: (state, action) => {
      state.value.push(makeTimer(action.payload))
    },

    toggleTimer: (state, action) => {
       state.value[action.payload].isRunning = !state.value[action.payload].isRunning
    },	
  },
})

...
```

The first action `addTimer` adds a new timer to the timers array. An action is a function that define `state` and an `action` as parameters. You can see that state defined in `initialState` is an array, so the `state` parameter of this function is that array. 

This function creates a new timer and pushes it into the array. 

The `payload` will contain the name of the new timer. Remember `createTime` needs a name. 

The `toggleTimer` function has the job of changing/toggling the state of a timer's `isRunning` property. 

Since the timers are in an array and we will want to target one of the timers in the array the payload will contain the index of the timer we are targeting. 

Export your actions, edit the following: 

```JS
...

export const { addTimer, toggleTimer } = timersSlice.actions

...
```

**Redux state cna only be changed from an action!** That's why Redux is called a "predictable state container". The only way to change the taimers is list is by using the `addTimer` or `toggleTimer` actions. And these are the only changes that can be made! If you want to make other changes, like removing a timer, you would need to define a new action here! 

## Wrapping up this section

There is nothing that will be visible in the app so far. You need to write some more code to make use of what you have done here. Your code should compile without errors. 

## Technical Planning

1. ~~Review Project~~
2. ~~Create timer objects~~
3. **Setup Redux Toolkit**
4. Setup React Redux Provider
5. Create New Timer Component
6. Create List Timer Component
7. Create Timer View Component
8. Keeping Time
9. Format Time
10. Styling the App
11. Persisting Timers
12. Stretch Goals

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'added Timer actions'
$ git push
```
