# Comprehensive review of React state updates

In React, State update is the critical mechanism driving component rendering. State can be managed and updated using different ways in class and functional components. The following is a comprehensive review and summary of React state updates, including class components, functional components, and state updates for arrays and objects.

## Review

1. **Regarding state updates of arrays**

   1. **Add elements**: using the spread operator, `[...arr, newElement]`
   2. **Remove elements**：using the filter method, `arr.filter(item=>filter condition)`
   3. **Modify elements**：using the map method+tenary operator，`arr.map(item=>Whether found the target?new element : item)`

2. **Regarding state updates of objects**

   1. **Add or modify properties**: Use the spread operator and replace old properties with new ones.

      ```tsx
      setState({...oldObject, newProp:newValue})
      ```

   2. **Remove properties**: Use the spread operator to extract the properties that need to be retained, and then return them.

   ```tsx
   const {needDeleteProp, ...otherProps} = oldObject
   setState({...otherProps})
   ```

## State updates in class components

#### 1. State Initialization

- initialize state within a constructor function.
- initialize state using class literal syntax.

```jsx
// Use construtor function to initialize state.
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
}

// Use the class field syntax to initialize state.
class MyComponent extends React.Component {
  state = {
    count: 0
  };
}
```

#### 2. State Updates

- Use the `this.setState` method.
- `this.setState` can accept an object or a function as its parameter.

```jsx
// Use an object as its parameter
this.setState({ count: this.state.count + 1 });

// Use a function as its parameter
this.setState((prevState) => ({ count: prevState.count + 1 }));
```

#### 3. Update the state of arrays and objects

- For updating the state of arrays and objects, you need to create a new array or object to ensure following the immutability principle.

```jsx
// 更新数组

// 添加元素
this.setState((prevState) => ({
  items: [...prevState.items, newItem]
}));

// 删除元素
this.setState((prevState) => ({
  items: prevState.items.filter((_, index) => index !== itemIndexToRemove)
}));

// 修改指定索引的元素
this.setState((prevState) => ({
  items: prevState.items.map((item, index) => 
    index === itemIndexToModify ? newValue : item)
}));
```



```js
// 更新对象

// 添加或更新属性
this.setState((prevState) => ({
  user: { ...prevState.user, name: 'New Name' }
}));

// 删除属性
this.setState((prevState) => {
  const { email, ...updatedUser } = prevState.user;
  return { user: updatedUser };
});

// 修改指定属性
this.setState((prevState) => ({
  user: { ...prevState.user, age: newAge }
}));
```



## State updates in functional components

#### 1. Use useState to initialize state

- Use `useState`hook to initialize state.
- `useState` returns an array including the current state and the function to update state.

```jsx
import React, { useState } from 'react';

const MyComponent = () => {
  const [count, setCount] = useState(0);
  return <div>{count}</div>;
};
```

#### 2. State updates

- Call the state update function to update state.
- The state update function can accept a new state value or a callback function.

```jsx
// set new state directly
setCount(count + 1);

// use a callback function
setCount((prevCount) => prevCount + 1);
```

#### 3. Update state of arrays and objects

- For updating the state of arrays and objects, it's also necessary to create a new array or object to ensure the immutability principle.

```jsx
// ====== Update arrays ======

// update an array
const [items, setItems] = useState([]);

// add an element
setItems((prevItems) => [...prevItems, newItem]);

// remove elements
setItems((prevItems) => prevItems.filter((_, index) => index !== itemIndexToRemove));

// Modify the element at the specified index
setItems((prevItems) =>
  prevItems.map((item, index) => (index === itemIndexToModify ? newValue : item))
);

// ====== Update obejcts ======

// add or update properties
setUser((prevUser) => ({ ...prevUser, name: 'New Name' }));

// remove properties
setUser((prevUser) => {
  const { email, ...rest } = prevUser;
  return rest;
});

// modify the specified properties
setUser((prevUser) => ({ ...prevUser, age: newAge }));
```

## Use `useReducer` to manage complex state

#### 1. Initialize state

- Define the state and action type
- Use `useReducer` hook

```jsx
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

const MyComponent = () => {
  const [state, dispatch] = useReducer(reducer, initialState);
  return <div>{state.count}</div>;
};
```

#### 2. Trigger state updates

- Call the`dispatch` function to pass action objects.

```jsx
// trigger state updates
dispatch({ type: 'increment' });
dispatch({ type: 'decrement' });
```

### The best practice of state updates

1. **Maintain state immutability**：In both class and functional components, always ensure state immutability by updating the state through creating new arrays or objects.
2. **Use callback functions**：When updating state, using callback functions can ensure correctness in scenarios of asynchronous updates, especially when the new state relies on the previous state.
3. **Split up complex state**：For complex states, you can use multiple `useState` hooks or manage with the `useReducer` hook.
4. **Avoid unnecessary state updates**: In class components, avoid unnecessary state updates by comparing the differences between `prevState` and `this.state`. In functional components, check for dependency items with the `useEffect` hook.

### Summary

- **Class components**: Initialize state through constructor functions or class field syntax, update state with `this.setState`. Ensure creating a new array or object when updating state.
- **Functional components**: Initialize and update state with the `useState` hook. Ensure creating a new array or object when updating state.
- **Complex state management**: Use the `useReducer` hook to manage complex state, updating state by defining actions and state transition logic.

Understanding and mastering the state update mechanism is key to developing React applications. You can ensure the correctness of state updates and the performance of the application by following best practices.

