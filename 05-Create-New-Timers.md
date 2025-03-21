# 🆕 P05 – Create New Timers

Now that we can add timers to our Redux state, let’s improve the UI by **breaking out each timer into its own component** and giving it the ability to **pause, resume, and reset**.

---

## 1️⃣ Create a `TimerCard` Component
This component will represent a single timer and provide controls.

### Create a file: `src/components/TimerCard.js`

```jsx
import React from "react";
import { useDispatch } from "react-redux";
import { pauseTimer, resumeTimer, resetTimer } from "../features/timers/TimerSlice";

const TimerCard = ({ timer }) => {
  const dispatch = useDispatch();

  const handlePause = () => dispatch(pauseTimer(timer.id));
  const handleResume = () => dispatch(resumeTimer(timer.id));
  const handleReset = () => dispatch(resetTimer(timer.id));

  const elapsedSeconds = Math.floor(timer.elapsed / 1000);

  return (
    <div style={{ border: "1px solid #ccc", padding: 10, marginBottom: 10 }}>
      <h3>{timer.label}</h3>
      <p>Elapsed Time: {elapsedSeconds}s</p>
      <p>Status: {timer.isRunning ? "Running" : "Paused"}</p>
      {timer.isRunning ? (
        <button onClick={handlePause}>Pause</button>
      ) : (
        <button onClick={handleResume}>Resume</button>
      )}
      <button onClick={handleReset}>Reset</button>
    </div>
  );
};

export default TimerCard;
```

📌 **What This Does:**
- Displays the current status of a timer
- Lets the user pause/resume/reset using Redux actions

💡 **AI Prompt:** “How can I conditionally render buttons in React?”

---

## 2️⃣ Update `TimerBoard` to Use `TimerCard`

Modify `TimerBoard.js` to use your new component:

```jsx
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { addTimer } from "../features/timers/TimerSlice";
import TimerCard from "./TimerCard";

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
      <div>
        {timers.map((timer) => (
          <TimerCard key={timer.id} timer={timer} />
        ))}
      </div>
    </div>
  );
}

export default TimerBoard;
```

✅ **Checkpoint:** You should now be able to:
- Add multiple timers
- Pause/resume/reset each one independently

---

## 🧠 Stretch Challenges
- [ ] Use styled-components or CSS modules for `TimerCard`
- [ ] Add a delete button for each timer
- [ ] Display a running total of all active timers

---

## ➡️ Next Step
Now let’s make the timers actually **tick every second** using `setInterval`. Continue to [P06 – List Timers](06-List-Timers-and-Real-Time-Updates.md).
