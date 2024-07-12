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
// memoizedValue 只会在 a 或 b 改变时重新计算
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
// memoizedObject 在组件生命周期内保持不变
```

## Example Code

The following are some code examples of using `useMemo` to demonstrate how to optimize performance with it:

### Example 1：Avoid expensive calculations

```js
import React, { useMemo, useState } from 'react';

const ExpensiveComponent = ({ a, b }) => {
  const expensiveValue = useMemo(() => {
    console.log('Calculating expensive value...');
    return a + b; // 这里可以是更复杂的计算
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

`useMemo` 是一个强大的工具，用于优化性能，通过记忆某些计算结果，避免不必要的重新计算。Understanding when to use `useMemo` and how to use it to optimize React application performance is an important skill for writing efficient React components. 请注意，不要滥用 `useMemo`，只在确实有性能瓶颈的情况下使用它。