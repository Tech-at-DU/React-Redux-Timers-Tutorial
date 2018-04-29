---
title: "React Redux Timers - Style Timer View"
slug: react-redux-timers-style-timer-view
---

This section will talk about styling the Timer view 
component. 

# Define Class Names

Again following the BEM system. I started with this 
markup. 

```jsx
<div className='timer-view'>
  <div>
    <h2 className='timer-view-name__h2' />
    <h1 className='timer-view-time__h1' />
  </div>
  <button className='timer-view__button'/>
</div>
```

## Style the Block

I used Flex Box to layout the block. 

```css
.timer-view {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: stretch;
  padding: 1em;
}
```

By declaring this element as `display:flex` it becomes a
flex container and it's children become flex items. 

The child elements in this case are: 

- `<div>`
- `<button>`

`flex-direction:row` arranges the elements on the 
horizontal axis. 

`justify-content: space-between` adds any extra space 
between the flex items with no space on the outside
(far left and right).

`align-items: stretch` stretches flex items to fill the 
container from the top to the bottom. This property 
controls the cross-axis. 

## Style the Name and Time

```css
.timer-view-name__h2 {
  margin: 0;
  font-size: 1.25em;
}

.timer-view-time__h1 {
  margin: 0;
  font-size: 2em;
}
```

The headings h1 - h6 all have margin on the top and bottom.
I removed that set the size of the font to something I 
thought looked nice. 

When the `em` unit sets the size based on the base font
size. Setting fonts in this way is good practice. You 
can control the size of both elements by setting the 
`font-size` on the body element. For example, if the 
font size of the body element were `12px`, the h2 would 
appear as 15px and h1 would be 24px. 

## Style the button

```css
.timer-view__button {
  width: 78px;
  display: block;
  font-size: 1em;
  font-weight: bold;
  border: 1px solid #000;
  border-radius: 0.5em;
}
```

I wanted the button to have it's height and width to be
equal. There is no CSS property, or generally easy way 
to do this. There are some [hacks](https://www.w3schools.com/howto/howto_css_aspect_ratio.asp).

To keep things simple I just measured the height of the 
container and set the height in px. 

## BEM Modifers

Some classes are used to modify an element. For example you
might have a class that styles a button and another class
that modifys buttons when they are disabled, or used for 
dangerous operations such as deleting. 

In the BEM system you'll put the modifier at the end of the 
class name and separate it with two hyphens. For example: 

```css
.button {}
.button--disabled {}
.button--dangerous {}
```

These two styles will be used to invert the colors of the 
button when the timer is running or stopped. 

```css
.timer-view__button--start {
  color: #000;
  background-color: #fff;
}

.timer-view__button--stop {
  color: #fff;
  background-color: #000;
}
```

To make these styles useful they need to be applied to the
element in code. The buttons are dynamic and change state 
the classes need to be swapped when the button changes
state. 

In render method of 'view-timer.js' add soemthing like: 

`const buttonClass = isRunning ? "stop" : "start";`

This will get the name 'stop' or 'start' depending on the 
value of `isRunning`. 

Next in the JSX block find the button `className` and 
modify it to something like: 

```JSX
className={`timer-view__button timer-view__button--${buttonClass}`}
```

## Challenges 

Make the styles your own. These are pretty simple. You 
can do more and improve the appearance. 

## Resources 

- https://www.w3schools.com/css/css3_flexbox.asp


