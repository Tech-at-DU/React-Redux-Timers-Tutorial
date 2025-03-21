# 🚀 P10 – Stretch Goals

Congrats on building a fully functional, styled timer app with React and Redux! 🎉  
Now, let’s take it further with some **stretch goals** to challenge your skills and creativity.

---

## 🧠 Feature Ideas

### 🔁 1. Restart Timer
Add a button that fully restarts a timer from zero:
```js
restartTimer: (state, action) => {
  const timer = state.find(t => t.id === action.payload);
  if (timer) {
    timer.elapsed = 0;
    timer.startTime = Date.now();
    timer.isRunning = true;
  }
},
```
📌 Useful for Pomodoro-style cycles.

---

### ✏️ 2. Edit Timer Labels
Let users rename timers inline:
- Use an input that toggles with a double-click
- Dispatch a new `renameTimer` action in your slice

💡 *AI Prompt:* “How can I create an editable label input in React?”

---

### 🗂️ 3. Add Timer Categories
Organize timers by task type (e.g. Work, Break, Study):
- Add `category` to each timer object
- Filter and render timers by category in `TimerBoard`

---

### ⏳ 4. Countdown Mode
Let users start a timer with a target duration:
- Add a `countdownFrom` field to timers
- Show remaining time instead of elapsed
- Play a sound when time runs out

🎧 *Bonus:* Use the Web Audio API to beep or alert when done

---

### 🌗 5. Add Dark Mode
Add a toggle to switch between light/dark themes:
- Use CSS variables for color schemes
- Store user preference in `localStorage`

📌 Tip: You can also use a library like `styled-components` or `tailwindcss`.

---

### 📦 6. Data Export / Import
Let users:
- Export timers to JSON
- Import timers from a saved backup

```js
const json = JSON.stringify(timers);
const imported = JSON.parse(json);
dispatch(loadTimers(imported));
```

🧪 Great for long-term tracking or restoring state across devices.

---

## 💬 More Ideas
- ⏱️ Add lap functionality (record split times)
- 🔒 Lock a timer so it can’t be edited or deleted
- 📊 Show statistics (total time, average session length)
- ⏯️ Global controls: pause/resume/reset all timers

---

## 🎯 Challenge Yourself
Pick 2–3 of the above and implement them! These stretch goals give you:
- More practice writing Redux actions
- More UI state handling with React
- Creative freedom to explore ideas

✅ Ready to go even further? Build your own feature from scratch!

---

## ➡️ Next Step
In [P11 – Final Thoughts](11-Final-Thoughts.md), we’ll wrap up the project and look ahead to what you can build next!

