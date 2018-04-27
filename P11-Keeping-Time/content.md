---
title: "React Redux Keeping Time"
slug: react-redux-keeping-time
---

# Keeping Time

Keeping time is an important part of this app. It's also a big subject 
in JavaScript with many applications. 

JavaScript provides two methods and one Object for keeping time. 

## setTimeOut

`setTimeOut` : This method provides a one time callback after an 
interval. 

`setTimeOut(callback, milliseconds)`

The callback is a function that will be executed after a wait in 
milliseconds. There are 1000 milliseconds to a second. The callback is
executed once, and is not repeated. 

## setInterval

`setInterval` : This method provides a callback that repeats forever
after an interval. 

Like setTimeOut setInterval executes the callback after the interval.
Unlike setTimeOut setInterval continues executing the callback after 
each interval until cleared with clearInterval. 

## Date

The Date object creates a Date instance which represents a single moment
in time. Dates are stored as an integer value equal to the number of seconds 
since January 1, 1970 (the [Unix Epoch](https://en.wikipedia.org/wiki/Unix_time)).

A date object not only represents the date, it also represents the time 
in hours, minutes, seconds, and milliseconds. 

The Date Object provides a long list of methods that allow you to use for 
wide range purposes. 

We can use a couple features of Date for this project. 

## Keeping track of time in milliseconds

While setTimeOut and setInterval both claim to call you back after a set number 
of milliseconds in practice the CPU is a messy place with a lot going on 
and the times are not as accurate as you might think. 

here is an [example](https://repl.it/@MitchellHudson/setInterval-delta-time). 
You can test the example for yourself. Here is the output I got. 
The script uses 'setInterval' to log every 1000 milliseconds. 

The first column
is the cound, this should be seconds. 

THe second column is the actual number of milliseconds that have elapsed 
since the last interval. You'll see this vary. 

The right column is the total lapsed time. Notice that after 30 seconds 
the lapsed time is off by half a second! Might not seem like much but, it
would definitely be a problem for many applications. 

```JavaScript
1 1002 1002
2 999 2001
3 1001 3002
4 1000 4002
5 1001 5003
6 1001 6004
7 1026 7030
8 1020 8050
9 1020 9070
10 1019 10089
11 1021 11110
12 1020 12130
13 1019 13149
14 1020 14169
15 1020 15189
16 1021 16210
17 1019 17229
18 1020 18249
19 1021 19270
20 1020 20290
21 1019 21309
22 1020 22329
23 1020 23349
24 1021 24370
25 1019 25389
26 1020 26409
27 1020 27429
28 1020 28449
29 1019 29468
30 1020 30488
31 1021 31509
```

Calculating seconds based directly on callbacks from 'setInterval' Something 
like the script below would be like using the first column. As you can see from
the output above the results are not very accurate.

```JavaScript
var secs = 0
setInterval(() => {
  secs += 1
  console.log(secs)
  // do something every ~second
}, 1000)
```

A better method is to keep track of the time that has elapsed in milliseconds
by getting the difference in in time between callbacks from 'setInterval'. 
This called delta time. 

var time = 0 
var lastUpdate = Date.now()

```JavaScript
setInterval(() => {
  var now = Date.now()
  var dt = now - lastUpdate
  time += dt
  lastUpdate = now
  console.log(count, dt, time)
}, 1000)
```

Here time is calculated by getting the current time in ms (now - Date.now()). 
Then finding the difference in time since the last update (now - lastUpdate). 
This is delta time and is the number of milliseconds since the last update. 
The example above adds this to time to calculate the elapsed time. 

The method above gives a very accurate representation of time. 

## store.dispatch()

In some cases you will want to dispatch actions to the store without 
sending them from a view. For example, you need to update the store every 
second from a setInterval callback. 

To do this use: 

`store.dispatch(action)` 

Where action is an action object with a type. Best practice would be 
to call an action creator to generate the action Object!

## Challenges 

Add a new action type: 'UPDATE' to 'src/actions/index.js'

Define an action creator for the 'UPDATE' action. This action Object
only needs a type, it won't need a paylod. 

Now, update 'src/reducers/timers-reducer.js'. The reducer function 
needs to handle the new actions 'UPDATE' action. 

## Resources 

- 



