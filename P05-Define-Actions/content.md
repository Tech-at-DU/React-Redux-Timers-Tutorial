---
title: "React Redux Defining Actions"
slug: react-redux-defining-actions
---

# Defining Actions

Your app needs to manage data. The data will stored with Redux 
as part of the store. The Flux pattern and Redux require that 
you define actions that describe how data can be modified.

**Data can only be modifed through actions.**

For this project you will start by defining the actions before 
making the app! 
 
You will need to do the following things with the store in the app. 
 
- Create a new timer
- Reset a timer 
- Delete a timer
- Start a timer 
- Stop a timer 
- Toggle a timer 
- Select a timer 
 
There may be other actions but these will all you to 

Create new timers. Creating a timer will add a new timer object to 
an array of timer objects held by the store. 

Reset a timer to 0. This action will require the index of that timer. 

Delete a timer. Removes a timer from the array of timers in the 
store. This will require the index of the timer. 

Start a timer. This action starts a timer running, and requires the 
index of the timer to start. 

Stop a timer. Stops a timer at the current time. This requires 
the index of the timer. 

Toggle timer, starts or stops a timer. This requires the index of 
the timer. 

Select timer, selects a timer. Selecting a timer will display 
details about that timer. This requires the index of the timer. 

Each action should be defined as a `const` with string value.  

**Defining action Creators**

You will also need to define some action creators. One for each 
action. An action creator is a function that returns an object 
with a type, and a payload when a value needs to accompany the
action. 

## Challenges 

Create folder: 'src/actions', and then add file: 'src/actions/index.js'. 

Define all of the actions above in 'src/actions/index.js'

Add an action creator for each action type in 'src/actions/index.js'

Be sure to export each action and each action creator. You will need 
access to these in other modules. 

## Resources 

- 



