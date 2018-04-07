---
title: "React Redux Setup Provider"
slug: react-redux-setup-provider
---

# Setup the provider

React Redux gives us the Provider component. Provider takes 
a redux store as a prop and provides access to the store to 
all of the child components. 

You will want to define Provider as high up your component 
hierarchy as you can. App.js makes a good place for this. 

## Challenges 

Import 'createStore' from Redux and 'Provider' from React Redux. 

```JavaScript
import { createStore } from 'redux'
import { Provider } from 'react-redux'
```

Next import your Reducers from 'src/reducers'.

```JavaScript
import reducers from './reducers'
```

Testing your project here will detect if there any problems 
in your reducers. Solve any errors that might appear. 

Next, define your store. 

```JavaScript
const store = createStore(reducers)
```



## Resources 

- 



