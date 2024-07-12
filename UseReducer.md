# Reducer+TS

1. Define a function called xxReducer。
   1. **Parameter 1：state**，The state interface (XxxState) needs to be defined separately.
   2. **Parameter 2：action**，The action type (XxxAction) needs to be defined separately (union type + type and payload properties).
   3. **Function body**: Switch on `action.type`, returning a new state for each case, and return the default state for `default`.
2. Call the `useReducer` hook.
   1. **Parameter 1**: The reducer function object.
   2. **Parameter 2**: The initial value.
   3. **Returning Value**: An array, where index 0 is the state value, and index 1 is the dispatch function object.
3. Dispatch message to trigger modification:
   1. Call dispatch and pass in the corresponding action object.

```tsx
// Define state and action types
interface XxxState {
  // define state properties here
}

type XxxAction =
  | { type: 'ACTION_TYPE_ONE'; payload: any }  // specify payload type as needed
  | { type: 'ACTION_TYPE_TWO'; payload: any }
  | { type: 'DEFAULT'; payload?: any };

// Define the reducer function
function xxReducer(state: XxxState, action: XxxAction): XxxState {
  switch (action.type) {
    case 'ACTION_TYPE_ONE':
      // Logic for ACTION_TYPE_ONE
      return { ...state, /* updated properties */ };
    case 'ACTION_TYPE_TWO':
      // Logic for ACTION_TYPE_TWO
      return { ...state, /* updated properties */ };
    default:
      // Return default state if no action matches
      return state;
  }
}

// Usage of useReducer hook in a React component
function MyComponent() {
  const [state, dispatch] = useReducer(xxReducer, { /* initial state */ });

  // Function to dispatch actions
  function triggerModification() {
    dispatch({ type: 'ACTION_TYPE_ONE', payload: {/* payload data */} });
    // You can call dispatch as needed with the appropriate action objects
  }

  return (
    <div>
      {/* Component JSX with state and dispatch logic */}
    </div>
  );
}
```

