# Timer Object

## Defining the Timer Object

The app will create and store Objects that define a timer. Timer objects will have the following properties that will define it:

- **name:** String - the name of the timer
- **time:** Number - the time in milliseconds
- **isRunning:** Boolean - tracks whether the timer is running or paused

You can add more properties to expand the functionality of the app. For example you might have `billable`, and rate if the app was used for business.

JavaScript only has one `Object` type. It has many ways to create objects. For this tutorial we will be using the class syntax. This will follow the same coding style used for creating React components.

# Creating Timer Objects

In your `src` folder, create a `Timer.js`. Write a function that creates Timer objects. A timer object is a JS object with properties: `name`, `time`, and `isRunning`. The createTimer function receives the name as a parameter and sets default values for time and isRunning.
>
```js
class Timer {
  constructor(name) {
    this.name = name 
    this.time = 0 
    this.isRunning =false
  }
}

export default Timer
```

Below is an example on how to create an instance of `Timer`:

```js
const myTimer = new Timer('Workout');
```

Great work, this is just the beginning!

## Technical Planning

1. ~~Review Project~~
2. **Create timer objects**
3. Setup Redux Toolkit
4. Setup React Redux Provider
5. Create New Timer Component
6. Create List Timer Component
7. Create Timer View Component
8. Keeping Time
9. Format Time
10. Styling the App
11. Persisting Timers
12. Stretch Goals

## Resources

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes

# Now Commit

```bash
$ git add .
$ git commit -m 'added Timer class'
$ git push
```
