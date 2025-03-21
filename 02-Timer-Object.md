# ⏱️ P02 – Timer Object

In this step, we’ll define the **shape and logic** of a timer so we can track elapsed time and manage each timer's state using Redux.

Each timer will have:
- `id` – A unique identifier
- `label` – A name for the timer (e.g. "Writing", "Exercise")
- `startTime` – The timestamp when the timer starts
- `elapsed` – The amount of time tracked so far (in milliseconds)
- `isRunning` – Whether the timer is currently active

---

## 1️⃣ Define Timer Data Structure
Let’s define a `createTimer` function to generate new timer objects.

Create a file at: `src/features/timers/createTimer.js`

```js
export function createTimer(label = "Untitled Timer") {
  return {
    id: Date.now(),
    label,
    startTime: Date.now(),
    elapsed: 0,
    isRunning: true,
  };
}
```

📌 **Why use `Date.now()`?**
It gives us a quick, unique `id` and a timestamp in milliseconds.

📌 **AI Prompt:**
*"What’s the difference between `Date.now()` and `new Date()` in JavaScript?"*

---

## 2️⃣ Example Timer Output
```js
{
  id: 1712875400000,
  label: "Coding",
  startTime: 1712875400000,
  elapsed: 0,
  isRunning: true
}
```

🧠 We’ll use `startTime` to calculate elapsed time on the fly, then save it into `elapsed` when paused.

---

## 3️⃣ Future Enhancements
This structure is flexible and supports:
- ⏸️ Pausing/resuming
- ⏱️ Restarting from zero
- 📝 Adding categories or notes later

---

## ✅ Checkpoint
You should now have a utility that generates timer objects. We’ll add this into Redux in the next step.

---

## 💡 Stretch Challenges
- [ ] Add a `color` property to each timer
- [ ] Add an optional `notes` field for the timer
- [ ] Use `uuid` instead of `Date.now()` for `id`

---

## ➡️ Next Step
Continue to [P03 – Setup Redux Toolkit](03-Setup-Redux-Toolkit.md) to add Redux state for your timers!

