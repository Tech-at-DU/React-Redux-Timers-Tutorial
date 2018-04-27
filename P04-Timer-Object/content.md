---
title: "React Redux Timer Object"
slug: react-redux-timer-object
---

# Defining the Timer Object

The app will create and store Objects that define a timer. 
Timer objects will have properties that define the timer. 
These will be: 

- name: String - the name of the timer
- time: Number - the time in milliseconds
- isRunning: Boolean - tracks whether the timer is running or paused

You can add more properties to expand the functionality of the app. 
For example you might have billable, and rate if the app was used 
for business. 

JavaScript only hase one Object type. It has many ways to create 
objects. For this tutorial I'm going to suggest using the class
syntax. This will follow the same coding style used for creating 
React components. 

## Creating Classes 

Define a class the `class` keyword. The following example 
creates a class named Book. Class names by convention 
always start with an uppercase letter. 

```
class Book {

}
```

Initalize the properties of class in it's constructor 
function. 

```
class Book {
  constructor(name) {
    this.name = name;
    this.rating = 0;
    this.isRead = false;
  }
}
```

The `Book` class defines three properties. 

The `name` property is passed into the constructor shen 
the class is initialized. 

Create an instance of Book like this: 

```
var myBook = new Book('War and Peace');
```

## Challenges 

Define a class 'Timer'. 

The Timer class should define the following properties: 

- name: A String, this is the name given to a timer
- time: A Number, this holds how long the timer has been running
- isRunning: A Boolean, this determines whether a timer is running or not

## Resources 

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes



