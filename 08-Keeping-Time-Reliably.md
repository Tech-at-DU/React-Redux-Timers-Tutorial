# 🕒 P08 – Keeping Time (Reliably)

Timers are working, but there’s still a problem: if you refresh the page, **all timers reset**. In this step, we’ll preserve timer data using **localStorage**, and improve accuracy during pause/resume cycles.

---

## 1️⃣ Save Timer State in localStorage

### Step 1: Create a utility file `src/app/localStorage.js`
```js
export const loadState = () => {
  try {
    const saved = localStorage.getItem("timers");
    return saved ? JSON.parse(saved) : undefined;
  } catch (e) {
    console.error("Load error:", e);
    return undefined;
  }
};

export const saveState = (state) => {
  try {
    const json = JSON.stringify(state);
    localStorage.setItem("timers", json);
  } catch (e) {
    console.error("Save error:", e);
  }
};
```

### Step 2: Integrate with `store.js`
Update `src/app/store.js`:
```js
import { configureStore } from "@reduxjs/toolkit";
import timersReducer from "../features/timers/TimerSlice";
import { loadState, saveState } from "./localStorage";

const preloadedState = loadState();

export const store = configureStore({
  reducer: { timers: timersReducer },
  preloadedState,
});

store.subscribe(() => {
  const state = store.getState();
  saveState({ timers: state.timers });
});
```

✅ **Checkpoint**: Your timers now persist across reloads.

💡 **AI Prompt:** “Why is preloadedState important for Redux persistence?”

---

## 2️⃣ Improve Pause/Resume Accuracy
Our timers store `startTime` but we need to **accurately track elapsed time** across multiple pauses.

Let’s update the Redux slice to calculate elapsed time based on `startTime` only when `isRunning` is `true`, and preserve previous elapsed time when paused.

### In `TimerSlice.js`, update the `resumeTimer` reducer:
```js
resumeTimer: (state, action) => {
  const timer = state.find(t => t.id === action.payload);
  if (timer && !timer.isRunning) {
    timer.startTime = Date.now();
    timer.isRunning = true;
  }
}
```

🧠 We already handle adding `elapsed` time in `pauseTimer`, so this works well in tandem!

✅ **Checkpoint**: Timers don’t lose time after pausing and resuming.

---

## 🧠 Stretch Challenges
- [ ] Add a toggle to auto-save timer snapshots every minute
- [ ] Allow importing/exporting timer data as JSON
- [ ] Show a visual indicator that state is saved

---

## ➡️ Next Step
In [P09 – Format Time](09-Adding-Styles-and-Polish.md), we’ll refine display logic and give the UI some polish!