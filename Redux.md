# Redux Review 

## Creating a Store with createStore 

### Step One: Defining a Reducer to Create the Store

It is basically the same as the default method of creating a reducer. The only difference is that you need to pass in the default state value when defining the reducer, because `useReducer` will not be used. The default state value can be passed in as the second parameter. Pass this reducer into `createStore`, which returns a store, and then export the store.

### Step Two: Provider Component

Use the `Provider` component to wrap child components and pass in the `store` (this step is similar to `Context`).

### Step Three: Fetch state and dispatcher

Use `useSelector` and `useDispatch` to respectively get state and dispatch, similar to splitting up `useReducer` into two hooks.

> If it's a class component, you can get the state using `store.getState()`.

### Step Four：Dispatch

Dispatch actions using dispatch.



## Use ReduxToolkit to create store

一、Canceled the separate reducer and action files; created a slice using `createSlice` in the store file.

* Parameter 1：The slice name.

* Parameter 2：The initial state.

* Parameter 3：The Reducers object. pass in the action method inside. Template as follows:

  > action名称(state){
  > 	// 修改state，不需要返回(在Slice中可以直接修改状态)。
  > }

二、Export the action methods for dispatch use. Dispatch can still pass in actions, but you need to add the prefix `sliceName/`.

```tsx
export const { increment, decrement, reset, incrementByAmount } = counterSlice.actions;

<button onClick={() => dispatch(increment())}>Increment</button>

```

三、Use the `configureStore` method to pass in an object containing the reducer (with the value being the slice's reducer), and then return and export the store to be passed into the Provider.

```jsx
// store.js
import { configureStore, createSlice } from '@reduxjs/toolkit';

// 定义初始状态
const initialState = {
  // 通过useSelector(state=>state.count)来返回
  count: 0,
};

// 创建一个 slice
const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment(state) {
      state.count += 1;
    },
    decrement(state) {
      state.count -= 1;
    },
    reset(state) {
      state.count = 0;
    },
    incrementByAmount(state, action) {
      state.count += action.payload;
    },
  },
});

// 导出 action 方法，通过useDispatch()和dispatch(increment)来调用
export const { increment, decrement, reset, incrementByAmount } = counterSlice.actions;

// 配置 store
const store = configureStore({
  reducer: {
    counter: counterSlice.reducer,
    // 使用thunk以便在异步线程中使用dispatch
    middleware: (getDefaultMiddleware) => getDefaultMiddleware().concat(thunk),
  },
});

export default store;
```



## Middleware Review

Middleware is essentially an interceptor and plugin, intercepting and handling actions before they reach the reducer, and is used to enhance Redux functionality. For example: asynchronous operations, logging, error reporting, persistence, and so on.

> ```
> dispatch(action) -> Middleware A -> Middleware B -> Middleware C -> reducer
> ```

```js
const middlewareA = store => next => action => {
  console.log('Middleware A: Before Action', action);
  const result = next(action); // pass to the next middleware
  console.log('Middleware A: After Action', store.getState());
  return result;
};

const middlewareB = store => next => action => {
  console.log('Middleware B: Before Action', action);
  const result = next(action); // pass to the next middleware
  console.log('Middleware B: After Action', store.getState());
  return result;
};

const middlewareC = store => next => action => {
  console.log('Middleware C: Before Action', action);
  const result = next(action); // pass to the next middleware
  console.log('Middleware C: After Action', store.getState());
  return result;
};
```



### Use middleware in createStore

Use the applyMiddleware method to pass in the necessary middleware, and then pass it as the second parameter to createStore.

```jsx
const store = createStore(
  rootReducer,
  applyMiddleware(loggerMiddleware)
);
```

### Config middleware in ReduxToolkit

```jsx
const store = configureStore({
  reducer: rootReducer,
  middleware: (getDefaultMiddleware) => getDefaultMiddleware().concat(logger, thunk)
});
```

### Config a custom middleware

```tsx
const loggerMiddleware = store => next => action => {
  // Record the action before it is passed to reducer.
  console.log('dispatching', action);
  // Pass the action to the next middleware or reducer (necessary code)
  let result = next(action);
  // Record the new state after the action is handled by reducer.
  console.log('next state', store.getState());
  return result; // Return the handled result of the action (optional but recommended).
};
```



## Review Action

1. An action is essentially a union type, with each type having a `type` property and an optional `payload` property.

2. The simplest definition approach:

   ```jsx
   type XxxAction = {type:"INCREMENT"} | {type:"DECREMENT"}
   
   type IncrementAction = { type: "INCREMENT" };
   type DecrementAction = { type: "DECREMENT" };
   
   type Action = IncrementAction | DecrementAction;
   ```

3. Optimization 1: You can put INCREMENT and DECREMENT into an enum to avoid hardcoding.

   ```ts
   enum ActionType {
     INCREMENT = "INCREMENT",
     DECREMENT = "DECREMENT"
   }
   
   type IncrementAction = { type: ActionType.INCREMENT };
   type DecrementAction = { type: ActionType.DECREMENT };
   
   type Action = IncrementAction | DecrementAction;
   ```

4. Optimization 2: You can extract `{type: "INCREMENT"}` and `{type: "DECREMENT"}` into a separate interface or type for standardization.

   ```ts
   enum ActionType {
     INCREMENT = "INCREMENT",
     DECREMENT = "DECREMENT"
   }
   
   interface IncrementAction {
     type: ActionType.INCREMENT;
     payload?: number; // You can add payload as needed
   }
   
   interface DecrementAction {
     type: ActionType.DECREMENT;
     payload?: number; // You can add payload as needed
   }
   
   type Action = IncrementAction | DecrementAction;
   ```

   