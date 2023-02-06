# List Timers

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
	const timers = useSelector(state => state.timers.value)
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

## Technical Planning

1. ~~Review Project~~
2. ~~Create timer objects~~
3. ~~Setup Redux Toolkit~~
4. ~~Setup React Redux Provider~~
5. ~~Create New Timer Component~~
6. **Create List Timer Component**
7. Create Timer View Component
8. Keeping Time
9. Format Time
10. Styling the App
11. Persisting Timers
12. Stretch Goals

# Now Commit

```bash
$ git add .
$ git commit -m 'added list of timers'
$ git push
```
