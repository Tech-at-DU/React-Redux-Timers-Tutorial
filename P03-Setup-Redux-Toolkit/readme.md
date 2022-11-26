# Setup Redux Toolkit

In this step you will setup Redux Toolkit. Along the way you'll create some folders to organize your code. 

You'll also create a file to manage a "slice" of your application state. Application state is stored in the the "store". The store is an object with many keys. The data store at one of these keys is a slice. This application will have a single slice "timers" that stores an array of the Timer objects you created in the last step. 

## Organize your code

Make a new folder: `src/features`

You'll store your helper files here. 

Create a new folder: `src/features/timers`.

This will store all of your timer related code in one place. 

Move `Timer.js` into: `src/features/timers`

Redux Toolkit organizes your application data in slices. You'll define each "slice" in a file. 

For this project you'll store a list of timers. This will be the Timers Slice! 

Add a new file `src/features/timers/timersSlice.js`

Add the following code: 

```JS
import { createSlice } from '@reduxjs/toolkit'
import Timer from './Timer'

const initialState = {
  value: []
}

export const timersSlice = createSlice({
  name: 'timers',
  initialState,
  reducers: {
    
  },
})

// Action creators are generated for each case reducer function
export const {  } = timersSlice.actions

export default timersSlice.reducer
```

What you are going to do is create an array of Timer objects that is managed by Redux. 

You will be able to add new timers to the list, start and stop timers in the list, and delete timers from the list. 

This "slice" that you have defined here will be responsible for managing these things. 

`initialState` defines the value stored as an empty array. 

The name of this "slice" of state is "timers".

Reducers are how state is modified. Currently your reducers are empty. 

Add two actions to the reducer: 

```JS
... 

export const timersSlice = createSlice({
  name: 'timers',
  initialState,
  reducers: {

    addTimer: (state, action) => {
      state.value.push(new Timer(action.payload))
    },

		toggleTimer: (state, action) => {
			state.value[action.payload].isRunning = !state.value[action.payload].isRunning
		},
		
  },
})

...
```

The first action `addTimer` adds a new timer to the timers array. An action is a function that takes state and an action. You can see that state defined in initialState is an array, so the state parameter of this function is that array. 

This function creates a new timer and pushes it into the array. 

The payload will contain the name of the new timer. This is a required parameter for creating a new timer!

The `toggleTimer` function has the job of changing/toggling the state of a timer's `isRunning` property. 

Since the timers are in an array and we will want to target one of the timers in the array the payload will contain the index of the timer we are targeting. 

Export your actions, edit the following: 

```JS
...

export const { addTimer, toggleTimer } = timersSlice.actions

...
```

## Wrapping up this section

There is nothing that will be visible in the app so far. You need to write some more code to make use of what you have done here. Your code should compile without errors. 

## Technical Planning

1. Review the Project
1. Install Tools
1. Define an Object to hold a Timer
1. Setup Redux Toolkit
1. Setup Redux Provider

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'added Timer actions'
$ git push
```
