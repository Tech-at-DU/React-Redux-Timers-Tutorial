# List Timers

## Technical Planning

1. ~~Build a Timer object~~
1. ~~Define the Actions of a Timer~~
1. ~~Define the Reducers of a Timer~~
1. ~~Allow users to create a Timer~~
1. **Allow users to see a list of Timers**
    1. Create a `list-timers` component that will house a list of timers
    1. Create a `timer-view` component to describe what a timer looks like
    1. Within the `timer-view`, allow for display of a name, time, and start/stop button
    1. Start/stop button should change text when clicked for now
    1. Display your progress so far in the browser
1. Users should be able to start/stop the clock on their Timers
1. Style the app
1. Allow Timers to persist

The list of timers will display all of the timers you have created. Each timer displayed in the list will need to display the following:

- Name
- Time
- Start/Stop - A button to start or stop that timer.

The Timer list itself should display the following:

- A list of timers in the store. Each timer will display a Name, Time, and start/Stop button.

# List-Timers - Boilerplate

Create a new file `src/components/ListTimers.js` with the following boilerplate code:

```js
import React from 'react'
import { useSelector } from 'react-redux'

export default function ListTimers() {
	
	return (
		<div>
			{/* render timers here */}
		</div>
	)
}
```

This base for the component imports `useSelector` from `react-redux`. This function is used to get your application state from the Redux store. 

## Accessing Application state

Add the following: 

```JS
export default function ListTimers() {
	const timers = useSelector(state => state.timers)
	...
```

Here is how you'll use use selector to get the list of timers from your Redux store. `useSelector()` takes a function as an argument: `useSelector(() => {})` and this function takes state as a parameter and returns the piece/slice of state you are interested in: `useSelector(state => state.timers)`. In this example you are returning the `timers` slice. 

## Display a list of timers

Add the following: 

```js
export default function ListTimers() {
	const timers = useSelector(state => state.timers.value)

	return (
		<div>
			{timers.map((timer, i) => {
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

## Displaying the list of timers

To display the list of timers you'll need to import the `TimerList` component into the `App` component and make an instance of it. 

In `src/App.js` and add the following:

```JS
...
import React from 'react';
import './App.css';
import NewTimer from './components/NewTimer';
import ListTimers from './components/ListTimers';

function App() {
  return (
    <div className="App">
      <NewTimer />
      <ListTimers />
    </div>
  );
}

export default App;
```

With this in place you should now see a new timer appear in the list each time you add one with the form above it. 

## Challenge

The markup that displays each timer in the list looks like: 

```JS
<div>
	<h2>{timer.name}</h2>
	<h1>{timer.time}</h1>
	<button>Start</button>
</div>
```

This would be better off as it's own component! This is the challenge! 

- Make a new component: TimerView
- It should take either a timer object or name, time, and isRunning as props. 
- It should display the: name, time, and a start/stop button
- Import this new component into the `ListTimers` component, and an instance for each timer in your list and pass the appropriate props. 

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'added list of timers'
$ git push
```
