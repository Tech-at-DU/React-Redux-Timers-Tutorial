# 🔗 P04 – Setup Redux Provider & Connecting UI

Now that the Redux store is configured, let’s connect it to our React components so we can **read from** and **write to** the timer state.

You’ll:
✅ Use `useDispatch` to dispatch Redux actions  
✅ Use `useSelector` to read timer state  
✅ Create a UI to add and view timers

---

## 1️⃣ Create a Basic Timer UI
Let’s build a component that displays a list of timers and adds new ones.

### Create a new file: `src/components/TimerBoard.js`

```jsx
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { addTimer } from "../features/timers/TimerSlice";

function TimerBoard() {
  const timers = useSelector((state) => state.timers);
  const dispatch = useDispatch();

  const handleAddTimer = () => {
    const label = prompt("Enter a timer label:") || "New Timer";
    dispatch(addTimer(label));
  };

  return (
    <div>
      <h2>All Timers</h2>
      <button onClick={handleAddTimer}>Add Timer</button>
      <ul>
        {timers.map((timer) => (
          <li key={timer.id}>
            <strong>{timer.label}</strong> — Elapsed: {Math.floor(timer.elapsed / 1000)}s
          </li>
        ))}
      </ul>
    </div>
  );
}

export default TimerBoard;
```

📌 **What This Does:**
- Uses `useSelector` to read the current timer state
- Uses `useDispatch` to create a new timer
- Renders a simple list of timers

💡 **AI Prompt:** "What does `useSelector` do in a React Redux app?"

---

## 2️⃣ Add `TimerBoard` to `App.js`

Update `App.js` to render your new component:

```jsx
import React from "react";
import TimerBoard from "./components/TimerBoard";

function App() {
  return (
    <div>
      <h1>Redux Timer App</h1>
      <TimerBoard />
    </div>
  );
}

export default App;
```

✅ **Checkpoint:** You should be able to add timers and see them appear in the list.

---

## 🧠 Stretch Challenges
- [ ] Display whether a timer is running or paused
- [ ] Style the `TimerBoard` with CSS modules or global styles
- [ ] Display the total number of timers

---

## ➡️ Next Step
In [P05 – Create New Timers](../P05-Create-New-Timers/readme.md), you’ll break out the **individual timer** into its own component and build controls to pause/resume/reset each timer!
