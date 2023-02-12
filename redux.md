### intro
- open-source javascript library for managing and centralizing your application state
- out of the box features with best practices, good behaviours, catching mistakes and simpler code


### 3 main components
- actions
  - sends data to the redux store
  - 2 properties
    ```js
    {
        payload: data_for_the_store, // type:[object, array, string]
        type: do_something_in_the_store // type: "string"
    }
    ```
- reducers
  - uses actions to know what to do with the redux store
  - action example, add, remove, update existing data in store
    ```js
    const reducer = (state, action) => {
        const {type, payload} = action
        // use the action to modify the state
    }
- store
  - only one store for any app
  - this is where we keep the application state
  - holds the states, and allows to access the state
  ```es6
  import {configureStore} from '@reduxjs/toolkit'

  const store = configureStore({
    reducer: reducer_value
  })

  store.getState()
  store.dispatch(action)
  ```
  - redux slices:
    ```
      import {configureStore} from '@reduxjs/toolkit'
      ...more
    ```

### setting up
- installation
  - `npm install @reduxjs/toolkit`
  - `npm install react-redux`
- folder structure
  - `./data/store.js`
  - the contents for `store.js` should be
    ```js
    import { configureStore } from "@reduxjs/toolkit";
    import { configure } from "@testing-library/react";

    const store = configureStore({
        reducer: {}
    })

    export default store;
    ```
- make these changes in the `index.js` file
    ```js
    import { Provider } from 'react-redux';
    import store from './data/store'

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(
    <React.StrictMode>
        <Provider store = {store}>
        <App />
        </Provider>
    </React.StrictMode>
    );
    ```

### working with redux toolkit
- 