# Setup Provider

One of the best features of using Redux is the ability to access your application state from any component. Making that happen requires the Provider component. Set this up now. 

## Setup provider

Make a new folder: `src/app`

Add a new file: `arc/app/app.js`

Add the following: 

```JS
import { configureStore } from "@reduxjs/toolkit";
import timersReducer from '../features/Timers/timersSlice'

export const store = configureStore({
	reducer: {
		timers: timersReducer
	}
})
```

Here you imported `createStore` from Redux toolkit and your reducers from your `timersSlice`. Then created your store and exported it. 

Now that the store is defined you need to initialize it and use the provider component to share the store with your entire app. 

The `timersReducer` is responsible for managing the list of timers, and the list of timers is accessed from the key `timers` on state. Think of this as a "slice" of state. 

Edit: `src/index.js`. Import some dependencies:

```JS
import { store } from './app/app';
import { Provider } from 'react-redux';
```

Next wrap your `<App />` component in the Provider component and set the `store` prop to your store.

```JS
...

root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);

...
```

Provider needs to be the parent of App, this allows it to pass the store down to it's descendents. 

## Testing your App

So far nothing visual and amazing will happen but your app should compile and run with out an error. Test it. If there is an error use the error messages to trace any issues. 

## Technical Planning

1. ~~Review Project~~
2. ~~Create timer objects~~
3. ~~Setup Redux Toolkit~~
4. **Setup React Redux Provider**
5. Create New Timer Component
6. Create List Timer Component
7. Create Timer View Component
8. Keeping Time
9. Format Time
10. Styling the App
11. Persisting Timers
12. Stretch Goals

# Now Commit


```bash
$ git add .
$ git commit -m 'added Timer reducers'
$ git push
```
