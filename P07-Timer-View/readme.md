# Timer List Item component 

If you solved the challenge in the last tutorial step you can compare your work agains what is in this step. Your solution doesn't have to match this, there is more than one way to solve the problem! 

## TimerView

Make a new file: `src/TimerView.js`. 

Add the following: 

```JS
import React from "react";

export default function TimerView({ timer }) {
	return (
		<div>
			<h2>{timer.name}</h2>
			<h1>{timer.time}</h1>
			<button>Start</button>
		</div>
	)
}
```

This component contains the markup from the previous example, and it's just the code that was inside `timers.map()`. 

Notice! I used a single prop `timer` which means that I planned to pass the timer object as a prop rather than the individual values. 

## Using the TimerView component

Edit `ListTimers.js`: 

```JS
...
import TimerView from './TimerView'

export default function ListTimers() {
	const timers = useSelector(state => state.timers.value)
	
	return (
		<div>
			{timers.map((timer, i) => <TimerView timer={ timer } />)}
		</div>
	)
}
```

This should now work the same as before. 

The difference in these changes is that you have separated the functionality of displaying the list of timers from the display of each List item. Now we can look at Timer List Items in one place: `TimerView.js` and look at displaying the whole list of Timers in another: `ListTimers.js`. 

## Improved props

We could improve the work above. Notice that passing the timer object: 

```JS
{timers.map((timer, i) => <TimerView timer={ timer } />)}
```

Focus on this: 

```JS
<TimerView timer={ timer } />
```

This means that you will have a prop named: `timer`. 

```JS
export default function TimerView({ timer }) {
	...
```

Which means that you need to use the dot notation to get at the: name, time, and isRunning properties. You can see that here: 

```JS
...
<h2>{timer.name}</h2>
<h1>{timer.time}</h1>
...
```

Make these changes. In `ListTimers.js`:

```JS
<TimerView {...timer} />
```

Here you are deconstructing the timer object into it's properties and passing these as props to the component. 

Next, in `TimerView.js` make the following changes: 

```JS
...
export default function TimerView({ name, time, isRunning }) {
	return (
		<div>
			<h2>{name}</h2>
			<h1>{time}</h1>
			<button>Start</button>
		</div>
	)
}
```

Notice that here you deconstructed to get the individual props. In the rest of the component you no longer need to use the dot notation! 

## Key prop Error 

You may be seeing: `Warning: Each child in a list should have a unique "key" prop.` This warning is telling us that we need to give each item in the list a unique key value. 

This is required by the virtual DOM to track changes efficiently. Read more here: https://reactjs.org/docs/lists-and-keys.html

Let's fix it. Edit `ListTimers.js`:

```JS
...
<div>
	{timers.map((timer, i) => <TimerView key={`timer-${i}`} {...timer} />)}
</div>
...
```

Each Timer Item component will have a key of `timer-#` where # is the index!

While we're hear for the next step to work each timer will need to know it's index in the list. To do this you need to add an index prop: 

```JS
<TimerView key={`timer-${i}`} index={i} {...timer} />
```

The new prop adds an index that is equal to the index of the timer in the lsit. 

## Displaying Start and Stop

The button for each timer currently displays "Start". The button needs to display "start" when `isRunning` is false and "stop" when `isRunning` is true! 

Edit `TimerView.js`:

```JS
...
	<button>
		{isRunning? "Stop" : "Start"}
	</button>
...
```

This is great but we need to change data in our application state when the button is clicked. 

To do this you need to use the dispatcher to send an action to the redux store. Just like adding a timer, like you did previously. This time the action will be the `toggleTimer` action. 

Edit `TimerView.js`. Import `useDispatch` and `toggleTimer` at the top: 

```JS
...
import { useDispatch } from 'react-redux'
import { toggleTimer } from "../features/timers/timersSlice"; 
...
```

Inside the component get the dispatcher: 

```JS
export default function TimerView({ name, time, isRunning }) {
	const dispatch = useDispatch()
	...
```

Be sure to add index to your list of props: 

```JS
export default function TimerView({ index, name, time, isRunning }) {
	...
```

Now call the dispatcher with your action on a button click: 

```JS
...
<button
	onClick={() => dispatch(toggleTimer(index))}
>
...
```

Test your work. Create a timer. Then click the start/stop button. The text should change from "start" to "stop" with each click. 

## Technical Planning

1. ~~Review Project~~
2. ~~Create timer objects~~
3. ~~Setup Redux Toolkit~~
4. ~~Setup React Redux Provider~~
5. ~~Create New Timer Component~~
6. ~~Create List Timer Component~~
7. **Create Timer View Component**
8. Keeping Time
9. Format Time
10. Styling the App
11. Persisting Timers
12. Stretch Goals

# Now Commit

```bash
$ git add .
$ git commit -m 'added timer view'
$ git push
```
