# 🎨 P09 – Adding Styles and Polish

Now that our timer app is functional and persistent, let’s make it feel **delightful to use**. In this step, we’ll:
✅ Add CSS for layout and visual clarity  
✅ Use reusable class names and responsive styling  
✅ Add animations for a more dynamic UI

---

## 1️⃣ Create a Global Stylesheet
Create a new file: `src/App.css`

```css
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f0f2f5;
  margin: 0;
  padding: 20px;
  color: #333;
}

h1, h2, h3 {
  color: #2c3e50;
}

button {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 8px 12px;
  margin: 5px;
  cursor: pointer;
  border-radius: 4px;
  transition: background 0.3s ease;
}

button:hover {
  background-color: #2980b9;
}

.timer-board {
  max-width: 600px;
  margin: auto;
}

.timer-card {
  background: white;
  padding: 16px;
  margin-bottom: 12px;
  border-radius: 6px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease;
}

.timer-card:hover {
  transform: translateY(-2px);
}
```

---

## 2️⃣ Apply the Styles in Components
### Update `App.js`
```js
import './App.css';
```

### Update `TimerBoard.js`
Add className:
```jsx
<div className="timer-board">
  {/* ... */}
</div>
```

### Update `TimerCard.js`
Add className:
```jsx
<div className="timer-card">
  {/* ... */}
</div>
```

✅ **Checkpoint**: Your timers now appear inside card-style containers with hover effects.

💡 **AI Prompt:** “What’s the difference between margin and padding in CSS?”

---

## 3️⃣ Bonus: Add Responsive Sizing
Want to support mobile screens? Add this to `App.css`:
```css
@media (max-width: 600px) {
  .timer-card {
    padding: 12px;
    font-size: 14px;
  }
}
```

✅ Now the app adapts to smaller screen sizes!

---

## 🧠 Stretch Challenges
- [ ] Add a dark mode toggle
- [ ] Use CSS animations to flash the timer when it’s paused/resumed
- [ ] Animate newly added timers (e.g., fade in or slide in)

---

## ➡️ Next Step
You’ve built a solid, styled app! In [P10 – Stretch Goals](10-Stretch-Goals.md), we’ll explore advanced features to take your timer app even further!
