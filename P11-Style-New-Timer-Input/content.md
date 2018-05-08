---
title: "React Redux Timers - Style New Timer Input"
slug: react-redux-timers-adding-styles
---

This section will talk about styling the input and 
button used to add a new timer. 

# Style the input 

In this section I'll walk through the methodology 
I used to apply CSS to the New Timer component 
and it's elements. 

## Class Naming: BEM

Using a good class naming system is important and 
will make your work easier and your project more 
organized. 

[BEM](http://getbem.com/introduction/) 
(Block Element Modifier) is a system that 
describes a best practice for creating class names. 
This section will apply BEM to the New Timer 
component. 

I started with: 

```HTML
<div>
  <input />
  <button />
</div>
```

I've left out all other features and am only showing
JSX elements here for clarity.  

```HTML
<div className='new-timer'>
  <input className='new-timer__input' />
  <button className='new-timer__button' />
</div>
```
Notice the child elements share the name of the 
parent block, in this case: 'new-timer'. Using the 
name of the component also makes sense here as it will 
help us recognize where these styles are applied. 

Names are lowercase and use a hyphen at the word break. 

Child elements are named with the block name followed
by the element name separated by two underscores. 

Why? If you know the system you can easily understand 
the HTML element structure by reading the CSS. 

Hyphens are used to separate words in a name. While the 
double underscore identifies the next item as the element. 

## Adding some style 

These are the styles I used. Feel free to use your own 
creative vision in your work. These ideas might be 
helpful or inspiring. 

I want the input and the button to be side by side. 
This will be easy in the case because both are 
[inline](https://www.w3schools.com/css/css_inline-block.asp) 
elements. 

**Style the block**

Inline elements should be held in a 
[block](https://www.w3schools.com/html/html_blocks.asp). 
The parent div provides this. 

I wanted to add some space arounf the whole block/group
so I added [margin](https://www.w3schools.com/css/css_margin.asp).

```css
.new-timer {
  margin: 1em;
}
```

**Style the Input Element**

I wanted the input to have larger text and have some space 
between the border and the text so I added padding. 

```css
.new-timer__input {
  padding: 0.5em;
  font-size: 1em;
}
```

Next I wanted to add a border and make round on the left.
I'll make the button round on the right and put the two 
elements side by side. 

```css
.new-timer__input {
  padding: 0.5em;
  font-size: 1em;
  border: 1px solid;
  border-radius: 0.5em 0 0 0.5em;
}
```

[border-radius](https://www.w3schools.com/cssref/css3_pr_border-radius.asp) 
rounds all the corners with a single value. 
Otherwise you can include a value that sets the radius for
all four corners. The first value is the upper left, and 
the values are applied clockwise. 

**Style the Button Element**

Next I want the button to be the same height as the input. 
By making the font and padding the same and giving it the
same border width it should do it. 

```css
.new-timer__button {
  border: 1px solid #000;
  font-size: 1em;
  padding: 0.5em;
}
```

I wanted the colors to be inverted compared to the input. 

```css
.new-timer__button {
  border: 1px solid #000;
  font-size: 1em;
  padding: 0.5em;
  background-color: #000;
  color: #fff;
}
```

Then I rounded off the two right corners. 

```css
.new-timer__button {
  border: 1px solid #000;
  font-size: 1em;
  padding: 0.5em;
  background-color: #000;
  color: #fff;
  border-radius: 0 0.5em 0.5em 0;
}
```


## Challenges 

Apply some styles your input. 

## Resources 

- http://getbem.com/introduction/
- https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/



