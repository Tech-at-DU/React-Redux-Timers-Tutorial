# Stretch Goals

Here are some more things you can try on your own to implement more features into this project. 

# Further challenges 

This app is small in scope but covers a wide range of technologies and has room to expand. Here are some ideas that you can explore. 

- The styles and uder interface could use improvements. Each peice of the interface is built as a component and each component has it's own stylesheet. 
- The state of each timer is on state and available to each component. It's possible to use this to change the appearance of each component. Imagine the start/stop button appears Green when it says "Start" and red when says "stop".
- Timers have a title and a time. It might be good if they had description below the title. To do this you'll need to modify the application state and interface. 
  - Add a new input for the description
  - The Timer class stores the title and time you'll need to expand this to support a description property. 
  - When creating a new Timer you're calling the NEW_TIMER/addTimer action you'll need to pass the description through here. 
  - A timer is created in the timerReducer modify this to add the new description. 
- It might be useful to have a reset button to reset a timer back to 0 for some uses.
  - Add a button to the TimerView
  - Create a new action RESET_TIMER and action creator function resetTimer.You'll need the index of the timer. Follow the pattern used by the start/stop buttons. 
  - Dispatch this action from your button.
  - Handle thie action in your timersReducer. 
- The times on all of the timers is data and reprents how much time was measured in a range of categories. You can create a new component to display this. Imagine a graph or a pie/donut chart showing the amount of time spent on each category. 
