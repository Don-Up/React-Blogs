# UseEffect

## Dependences

- If the dependency array is not specified, the callback function of useEffect is executed after each rendering.。
- If the dependency array is empty, the callback function of `useEffect` will be executed only once when the component is mounted and unmounted.
- If the dependency array contains specific values, the callback function of `useEffect` will be executed only when these dependency items change.

```js
// dependences are missing
useEffect(() => {
  console.log('Execute on each render');
});

// empty dependences
useEffect(() => {
  console.log('Execute only when the component is mounted and unmounted.');
}, []);

// specific dependences
useEffect(() => {
  console.log('Execute when the dependency changes.');
}, [dependency]);
```

## Clean up operation

You can return a function within the callback function of `useEffect`. The returned function will be executed when the component is unmounted or when dependency items change, and is used to clean up side effects.

```js
useEffect(() => {
  console.log('set subscription');

  return () => {
    console.log('cleanup subscription');
  };
}, [dependency]);
```

## Multiple useEffect

You can use multiple `useEffect` hooks within a component to handle different side effects or break down complex side effects.

```js
useEffect(() => {
  console.log('side effect 1');
}, [dependency1]);

useEffect(() => {
  console.log('side effect 2');
}, [dependency2]);
```

## Use `async/await` within  `useEffect` 

When using `async/await` within `useEffect`, you need to define an asynchronous function inside and call it, because the callback function of `useEffect` cannot be directly declared as `async`.

```js
useEffect(() => {
  const fetchData = async () => {
    const response = await fetch('/api/data');
    const data = await response.json();
    console.log(data);
  };

  fetchData();
}, [dependency]);
```

