# 🚀 P01 – Getting Started

Let’s kick off your timer app by setting up the React project and installing the required tools. This lesson covers:

✅ Creating a new React app  
✅ Installing Redux Toolkit and React-Redux  
✅ Structuring your folders for a clean project  

---

## 1️⃣ Create Your React App

Make sure you have **Node.js** and **npm** installed.

```bash
npx create-react-app timer-app
cd timer-app
npm start
```

📌 This creates a new React project called `timer-app`, moves into the directory, and starts the development server.

💡 Note! You can use another React starter project, like Vite if you like. Everything should work, though some names may differ. 

✅ **Checkpoint**: You should see the default React welcome screen in your browser.

---

## 2️⃣ Install Redux Toolkit

In the project directory, run:

```bash
npm install @reduxjs/toolkit react-redux
```

📌 **What This Does:**
- `@reduxjs/toolkit` simplifies Redux setup with slices and `configureStore`
- `react-redux` lets you connect your components to the Redux store

💡 **AI Prompt:** “What’s the difference between Redux and Redux Toolkit?”

---

## 3️⃣ Project Structure

Create the following folder structure inside your `src/` directory:

```
src/
├── components/         # Reusable UI components
├── features/           # Redux slices & logic (ex: timers/)
│   └── timers/
│       ├── TimerSlice.js
├── App.js
├── index.js
```

✅ This separation keeps your UI and logic modular and easier to scale.

💡 Note! You may have started with another React starter project and the files and structure may differ. Don't worry about that. 

---

## 4️⃣ App.js
Start by adding a title to the App component. 

### App.js
```jsx
function App() {
  return <h1>Timer App</h1>;
}

export default App;
```

### index.js
```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

✅ **Checkpoint**: Your browser should now show just a simple "Timer App" heading.

---

## 🧠 Stretch Challenges
Try these to solidify your setup:
- [ ] Add a `Header` component inside `components/`
- [ ] Create a basic CSS file and apply some styles
- [ ] Set up your project on GitHub and make your first commit

---

## 🎉 Next Step
Now that your environment is ready, we’ll define the **Timer data structure** in [P02 – Timer Object](02-Timer-Object.md).

Let’s start building!

