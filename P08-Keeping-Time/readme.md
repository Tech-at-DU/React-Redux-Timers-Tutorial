# Keeping Time

So far you have everything displaying, but the timers still aren't running. It's about time we fixed that and actually gave the start/stop buttons something to do!

# Update Action

These steps will walk through the whole Redux Toolkit ecosystem and offer some new ideas along the way!

Get started by adding a new action to your Timers Slice. Edit: `src/features/timers/timersSlice.js`:

```JS
  ...
  reducers: {

    ...

    update: (state, action) => {
      state.value.forEach(timer => {
        if (timer.isRunning) {
          timer.time += action.payload
        }
      })
    }
  },
  ...
```

Here you added a new action "update" and reducer function. This function loops over all of the timers in the list (`state.value`) and updates the time of each timer whose `isRunning` is true. The amount added to the time is from the payload. You'll be supplying this in a future step. Imagine that this is the amount of time that has passed since the last update. 

Export the `update` action at the bottom: 

```JS
...
export const { addTimer, toggleTimer, update } = timersSlice.actions
...
```

You need to issue update actions automatically and constantly. These won't be triggered by user interaction. You can do this with `setInterval`. Edit `src/app/app.js`. 

Import the new update action from your timers slice at the top: 

```JS
...
import { update } from '../features/timers/timersSlice'
...
```

Below the store add the following: 

```JS
let lastUpdateTime = Date.now()

setInterval(() => {
	const now = Date.now()
	const deltaTime = now - lastUpdateTime
	lastUpdateTime = now
	store.dispatch(update(deltaTime))
}, 500)
```

Here you defined a new variable: `lastUpdateTime`. This will store the time difference between each update action. 

Next you defined a new interval. The interval runs the callback function every 500 milliseconds. 

The callback function does these things: 

- Gets the current milliseconds with `Date.now()`
- Calculates the `deltaTime` 
- Sets the last `lastUpdateTime` to now
- Dispatches an `update` action with the `store.dispatcher()`

What you have done here is setup an action that will be dispatched every 500ms (half second).

## Test your work

Make two new timers. You'll see these in the list and the time should be 0. 

Click start on one of the timers. The button should change to "Stop" and the time should start incrementing at rough 500ms steps. 

The increment will not be perfect because timers are not perfect. It might show: 500, 1004, 1504, 2008 etc. 

You should be able to start and stop each timer. When timer is running the time should increase. When it's stopped the time should hold on it's previous time. 

## Displaying human readbale time

The time is currently shown in milliseconds. This is great for computers but humans like to read: hrs:mins:secs. 

Time is in milliseconds so divide by 1000 to get seconds, and divide by 60 to get minutes etc. 

From there you need to format the numbers. Imagine you you have the time 157598. How many seconds, minutes, hours are there?

- Seconds: 157598 / 1000 = 157.598
- Minutes: 157.598 / 60 = 2.6266333333
- Hours: 2.6266333333 / 60 = 0.04377722222

You need to round down at each step. Use `Math.round(n)`:

- Seconds Rounded: 157598 / 1000 = 157
- Minutes Rounded: 157.598 / 60 = 2
- Hours Rounded: 2.6266333333 / 60 = 0.0

Since we count seconds and minutes in units of 60 you should use modulous to count these in sets of 60.

> Modulous returns the whole number remainder. For example: 7 % 4 = 3 and 42 % 7 = 0. 

- Seconds: 157 % 60 = 37
- Minutes: 2 / 60 % 60 = 0
- Hours: 0 / 60 % 60 = 0

Try this on your own then check your solution against the example solution in the next tutorial page. 

challenge write a function that returns the formatted number. 

```JS
formatTime = (time) => { 
  ...
}

formatTime(157598) // 0:2:37
```

Stretch challenge: Format the numbers so that values below are padded with a 0. 

```JS
formatTime(157598) // 00:02:37
```

## Technical Planning

1. ~~Review Project~~
2. ~~Create timer objects~~
3. ~~Setup Redux Toolkit~~
4. ~~Setup React Redux Provider~~
5. ~~Create New Timer Component~~
6. ~~Create List Timer Component~~
7. ~~Create Timer View Component~~
8. **Keeping Time**
9. Format Time
10. Styling the App
11. Persisting Timers
12. Stretch Goals

# Now Commit

```bash
$ git add .
$ git commit -m 'timers running'
$ git push
```

