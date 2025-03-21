# 🔄 P06 – List Timers & Real-Time Updates

Currently, timers only show the static `elapsed` value from Redux. In this step, we’ll make the timers **update live** using `setInterval` and `useEffect`, so the elapsed time appears to tick forward every second while running.

---

## 1️⃣ Add Real-Time Display to `TimerCard`
We'll calculate the visible time by combining the stored `elapsed` value and the time since `startTime` **if** the timer is running.

### Update `TimerCard.js`
```jsx
import React, { useEffect, useState } from "react";
import { useDispatch } from "react-redux";
import { pauseTimer, resumeTimer, resetTimer } from "../features/timers/TimerSlice";

const TimerCard = ({ timer }) => {
  const dispatch = useDispatch();
  const [displayTime, setDisplayTime] = useState(timer.elapsed);

  useEffect(() => {
    let interval = null;

    if (timer.isRunning) {
      interval = setInterval(() => {
        const now = Date.now();
        const newElapsed = now - timer.startTime + timer.elapsed;
        setDisplayTime(newElapsed);
      }, 1000);
    } else {
      setDisplayTime(timer.elapsed);
    }

    return () => clearInterval(interval);
  }, [timer.isRunning, timer.startTime, timer.elapsed]);

  const handlePause = () => dispatch(pauseTimer(timer.id));
  const handleResume = () => dispatch(resumeTimer(timer.id));
  const handleReset = () => dispatch(resetTimer(timer.id));

  const elapsedSeconds = Math.floor(displayTime / 1000);

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
- Uses `useState` to manage locally displayed time
- Uses `useEffect` to tick every second and update UI
- Syncs with Redux state when paused/reset

💡 **AI Prompt:**
"What happens if you forget to clear an interval in `useEffect`?"

---

## 2️⃣ Test It Out
Run the app and:
- Add a few timers
- Watch them tick up in real-time
- Pause and resume to test logic

✅ **Checkpoint:** Each timer should update once per second while running.

---

## 🧠 Stretch Challenges
- [ ] Allow changing the update interval (e.g., faster/slower ticks)
- [ ] Use `Intl.DateTimeFormat` or a custom formatter to show HH:MM:SS
- [ ] Highlight timers that have been running for over 5 minutes

---

## ➡️ Next Step
In [P07 – Timer View](../P07-Timer-View/readme.md), we’ll focus on improving formatting, displaying time in a more readable format like `01:32:04`. Let’s go!

