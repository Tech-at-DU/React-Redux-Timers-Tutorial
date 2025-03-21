# 🧠 P03 – Setup Redux Toolkit

Now that we have a `createTimer` utility, it’s time to add **Redux Toolkit** to manage our timers.

We’ll:
✅ Create a Redux slice for timers  
✅ Add reducers to handle start/pause/reset  
✅ Configure the Redux store  

---

## 1️⃣ Create Your Timer Slice
Create a new file: `src/features/timers/TimerSlice.js`

```js
import { createSlice } from "@reduxjs/toolkit";
import { createTimer } from "./createTimer";

const timersSlice = createSlice({
  name: "timers",
  initialState: [],
  reducers: {
    addTimer: (state, action) => {
      state.push(createTimer(action.payload));
    },
    pauseTimer: (state, action) => {
      const timer = state.find(t => t.id === action.payload);
      if (timer && timer.isRunning) {
        timer.elapsed += Date.now() - timer.startTime;
        timer.isRunning = false;
      }
    },
    resumeTimer: (state, action) => {
      const timer = state.find(t => t.id === action.payload);
      if (timer && !timer.isRunning) {
        timer.startTime = Date.now();
        timer.isRunning = true;
      }
    },
    resetTimer: (state, action) => {
      const timer = state.find(t => t.id === action.payload);
      if (timer) {
        timer.elapsed = 0;
        timer.startTime = Date.now();
        timer.isRunning = false;
      }
    },
  },
});

export const { addTimer, pauseTimer, resumeTimer, resetTimer } = timersSlice.actions;
export default timersSlice.reducer;
```

📌 **This slice handles all the timer logic**:
- `addTimer` – Create a new running timer
- `pauseTimer` – Stop the timer and save elapsed time
- `resumeTimer` – Restart it from where it left off
- `resetTimer` – Start from zero

💡 **AI Prompt:** "Why is it okay to mutate state directly in Redux Toolkit slices?"

---

## 2️⃣ Configure the Store

Create a new file: `src/app/store.js`

```js
import { configureStore } from "@reduxjs/toolkit";
import timersReducer from "../features/timers/TimerSlice";

export const store = configureStore({
  reducer: {
    timers: timersReducer,
  },
});
```

✅ This registers the `timers` slice under `state.timers`

---

## 3️⃣ Provide the Store to React
Update `index.js`:

```js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { Provider } from "react-redux";
import { store } from "./app/store";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

📌 This gives your entire app access to Redux state and actions.

✅ **Checkpoint**: Your app compiles and runs with Redux configured.

---

## 🧠 Stretch Challenges
- [ ] Add a `removeTimer` reducer to delete a timer
- [ ] Sort the state by most recently started timer
- [ ] Log every action to the console (middleware)

---

## ➡️ Next Step
In [P04 – Setup Redux Provider](../P04-Setup-Provider/readme.md), we’ll connect our UI to Redux using hooks like `useSelector` and `useDispatch`. Let’s go!

