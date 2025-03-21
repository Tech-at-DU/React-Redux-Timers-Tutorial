# ⏰ P07 – Timer View and Formatting

Right now our timers display time in raw seconds. In this step, we’ll make the output **easier to read** by formatting the elapsed time as **HH:MM:SS** (hours, minutes, seconds).

We’ll:
✅ Create a `formatTime()` helper function  
✅ Use it in the `TimerCard` component  
✅ Optionally extract and reuse the formatter anywhere else

---

## 1️⃣ Create a Utility Function
Create a new file: `src/utils/formatTime.js`

```js
export function formatTime(ms) {
  const totalSeconds = Math.floor(ms / 1000);
  const hours = Math.floor(totalSeconds / 3600);
  const minutes = Math.floor((totalSeconds % 3600) / 60);
  const seconds = totalSeconds % 60;

  const padded = (n) => String(n).padStart(2, "0");

  return `${padded(hours)}:${padded(minutes)}:${padded(seconds)}`;
}
```

📌 **What This Does:**
- Converts milliseconds to hours, minutes, and seconds
- Adds zero-padding so values like `01:02:09` are aligned

💡 **AI Prompt:**
"How do I write a utility function in JavaScript that converts milliseconds into HH:MM:SS format?"

---

## 2️⃣ Update `TimerCard.js` to Use Formatter
Modify the line in `TimerCard.js` where we show `elapsedSeconds`.

First, import the utility:
```js
import { formatTime } from "../utils/formatTime";
```

Then replace:
```js
<p>Elapsed Time: {elapsedSeconds}s</p>
```
with:
```js
<p>Elapsed Time: {formatTime(displayTime)}</p>
```

✅ **Checkpoint:** Timers now display `00:01:32` instead of `92s`.

---

## 3️⃣ Improve Accessibility
You can add a `title` attribute so users can hover for the raw millisecond value:
```jsx
<p title={`${displayTime}ms`}>Elapsed Time: {formatTime(displayTime)}</p>
```

---

## 🧠 Stretch Challenges
- [ ] Highlight timers that reach 1 hour with a different style
- [ ] Add a tooltip showing raw milliseconds on hover
- [ ] Internationalize your formatter for different locales/time formats

---

## ➡️ Next Step
In [P08 – Keeping Time](08-Keeping-Time-Reliably.md), we’ll make our timers even more robust and explore how to keep time precisely across pauses and refreshes!

