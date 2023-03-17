## Introduction
- Redux (or standard Redux) is a state management library for js applications
- provides a state container and a way to manage the state in your application in a predictable and centralized way
- open-source javascript library for managing and centralizing your application state
- out-of-the-box features with best practices, good behaviors, catching mistakes and simpler code

### Introduction to Redux toolkit
- Redux toolkit provides a state of high-level APIs that abstract away many of the lower-level details of Redux
- these APIs make it easier to write Redux code by reducing the amount of boilerplate code you need to write
- provides built-in support for common use cases like creating **redux slices**
  - way to group related actions and reducers together
  - handling asynchronous actions with the `createAsyncThunk` API
  - provides a re-configured store that includes middleware and other configuration options that are commonly used in redux application
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
  - action example, add, remove, and update existing data in the store
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
        reducer: {
          cart: cartSlice.reducer,
          products: productSlice.reducer,
        }
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

### working with the redux toolkit
- creating redux actions and reducers
- exporting your redux actions and reducers
- updating your store  with the `useDispatch` hook
- getting data from your store with the useSelector hook
- displaying cart products from your redux store


### working with APIs in Redux Toolkit
- Redux toolkit provides builtin `createAsyncThunk`
```js
import {createAysncThunk} from '@reduxjs/toolkit';

const fetchAllProducts = createAysncThunk('fetch-all-products', async (apiUrl) => {
  const response = await fetch (apiUrl)
  return response.json()
})
const productSlice = createSlice({
  name: 'products',
  initialState: { data: [], fetchStatus: ""},
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchAllProducts.fulfilled, (state, action) => {
        state.data = action.payload
        state.fetchStatus= 'success'
    })
    .addCase(fetchAllProducts.pending, (state) => {
      state.fetchStatus = 'loading'
    })
    .addCase(fetchAllProducts.rejected, (state)=> {
      state.fetchStatus = "error"
    })
  },
})

export default productSlice;

```