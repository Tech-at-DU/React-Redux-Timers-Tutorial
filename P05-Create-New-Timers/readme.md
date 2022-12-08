# Creating new Timers

So far we have been working on getting Redux and React up and
running and no work has gone into components, which is the heart of React!

With actions and reducers in place you can now create
containers/components that display state from the store and
send actions to update the store. Let's get those working!

# New Timer Component

The first component we'll build is for creating new timers. The new timer component should have the following:

- A field to input a name
- A button to save the timer

> [info]
>
> The above field that will allow users to input a name is a **controlled component**. This is when "the React component that renders [an input] also controls what happens in that form on subsequent user input."
>
> You can read more about controlled components [here](https://reactjs.org/docs/forms.html#controlled-components)

Keep in mind that we won't see timers until the Timer list component is created, which will be built in the next chapter.

Create a new folder `src/components`. 

Create `src/components/NewTimer.js`. This file will define the new component. 

Add the followingL

```js
import React, { useState } from 'react'
import { useDispatch } from 'react-redux'

// We need to import our action to add a new timer
import { addTimer } from '../features/timers/timersSlice'

export default function NewTimer() {
	const [ name, setName ] = useState('')
	const dispatch = useDispatch()

	return (
		<div>

		</div>
	)
}
```

You now have a basic `NewTimer` component structure, but we have no idea how to render it! Remember we want to have the following:

- A field to input a name
- A button to save the timer

Fill in the `render` method in `NewTimer.js`, as well as adding a few other ancillary methods and an export statement:

```js
export default function NewTimer() {
	const [ name, setName ] = useState('')
	const dispatch = useDispatch()

	return (
		<div>

			<input
				type='text'
				placeholder="New Timer Name"
				name="name"
				value={name}
				onChange={(e) => setName(e.target.value)} />
			
			<button
				onClick={() => dispatch(addTimer(name))}
			>Save</button>

		</div>
	)
}
```

- `useDispatch` - Returns a reference to the dispatcher. The dispatcher allows you to send actions to the store to create changes in application state. 
- `useState` - is used to create a value that will be available across multiple renders of this component. Notice you used the controlled component pattern in the input!
- `dispatch(addTimer(name))` - Take a close loiok at this snippet of code. Let's break this one down. Clicking the button will add a new timer by calling the `addTimer(name)` action and passing the name as an argument. The value returned from this function call is then passed as an argument to a call to `dispatch(...new Timer...)`. This is how Redux works. To make a change to the application state, adding a new timer to the list of timers in this case, you will call one of the action functions and pass the reuslt to the dispatcher. 

## Display the New Timer Component

In order to see this new component in action you'll need to import it and create an instance. 

In `src/App.js` add the following: 

```JS
import React from 'react';
import './App.css';
import NewTimer from './components/NewTimer';

function App() {
  return (
    <div className="App">
      <NewTimer />
    </div>
  );
}

export default App;
```

With this in place you should see your new form. 

Test it out. You should be able to add a new timer but keep in mind that the new timers will not visible until we make a component to display them! 

Test your work and resolve any errors that appear in the console. 

## Technical Planning

1. ~~Review Project~~
2. ~~Create timer objects~~
3. ~~Setup Redux Toolkit~~
4. ~~Setup React Redux Provider~~
5. **Create New Timer Component**
6. Create List Timer Component
7. Create Timer View Component
8. Keeping Time
9. Format Time
10. Styling the App
11. Persisting Timers
12. Stretch Goals

# Now Commit

```bash
$ git add .
$ git commit -m 'added new timer input'
$ git push
```
