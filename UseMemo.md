# UseMemo

## Usage

`useMemo` is a React Hook used to optimize performance by memoizing certain calculated results, thus avoiding repeated calculations on each render. It takes a creation function and a dependency array, and it recalculates the returned value of the creation function only when the dependency items change.

```js
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

## Dependences

- If the dependency array is empty, the callback function of `useMemo` will be executed only once when the component is mounted, and it will memoize the returned value.
- If the dependency array contains specific values, the `useMemo` callback function will be executed again when these dependency items change, and it will update the memoized value.

```js
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
// memoizedValue is recalculated only when a or b changes.
```

## Performance Optimazation

- Using `useMemo` can avoid performing expensive calculations on each render, especially when the calculated results depend on values that change infrequently.
- Don't overuse `useMemo`; use it only when there is a real performance bottleneck. Otherwise, it will add unnecessary complexity.

## Differences from useEffect

- `useEffect` is used to handle side effects (such as data fetching and subscriptions) and does not return any value.
- `useMemo` is used to optimize calculations and return memoized values.

## Methods to update objects and arrays

- When updating objects and arrays, `useMemo` can help avoid unnecessary re-renders.

```javascript
const memoizedObject = useMemo(() => ({ a: 1, b: 2 }), []);
// memoizedObject remains unchanged throughout the component's lifecycle.
```

## Example Code

The following are some code examples of using `useMemo` to demonstrate how to optimize performance with it:

### Example 1：Avoid expensive calculations

```js
import React, { useMemo, useState } from 'react';

const ExpensiveComponent = ({ a, b }) => {
  const expensiveValue = useMemo(() => {
    console.log('Calculating expensive value...');
    return a + b; // More complex calculations can be performed here.
  }, [a, b]);

  return <div>Expensive Value: {expensiveValue}</div>;
};

const App = () => {
  const [count, setCount] = useState(0);
  const [a, setA] = useState(1);
  const [b, setB] = useState(2);

  return (
    <div>
      <ExpensiveComponent a={a} b={b} />
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <button onClick={() => setA(a + 1)}>Increment A</button>
      <button onClick={() => setB(b + 1)}>Increment B</button>
    </div>
  );
};

export default App;
```

### Example 2: Memoize objects

```js
import React, { useMemo, useState } from 'react';

const ComponentWithMemoizedObject = () => {
  const [count, setCount] = useState(0);

  const memoizedObject = useMemo(() => {
    return { key: 'value' };
  }, []);

  console.log('Component re-rendered');

  return (
    <div>
      <div>Memoized Object: {JSON.stringify(memoizedObject)}</div>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
    </div>
  );
};

export default ComponentWithMemoizedObject;
```

## Summary

`useMemo` is a powerful tool for optimizing performance by memoizing certain calculation results to avoid unnecessary recalculations. Understanding when to use `useMemo` and how to use it to optimize React application performance is an important skill for writing efficient React components. Please keep in mind, don't overuse `useMemo`; use it only when there are significant performance bottlenecks.