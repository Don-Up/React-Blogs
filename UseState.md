# UseState

## The parameter and return value of useState

`useState` takes a default value as a parameter and returns an array containing the state and a method to change the state.

```javascript
const [state, setState] = useState(defaultValue);
```



## You can pass a callback into the state method

The state method can accept a callback that takes the previous state as its parameter and returns a new state. This is very useful when you need to depend on the current state.

```javascript
setState(prevState => newState);
```



## `useState` can accept a callback that returns the initial value

The callback function is called only during the initial render and helps with performance optimization.

```javascript
const [state, setState] = useState(() => computeInitialState());
```



## The immutability principle should be followed when updating objects and arrays

When updating objects and arrays, create new objects and arrays to adhere to the immutability principle.

```javascript
// update objects
const [obj, setObj] = useState({ key: 'value' });
setObj(prevObj => ({ ...prevObj, key: 'newValue' }));

// update arrays
const [arr, setArr] = useState([1, 2, 3]);
setArr(prevArr => [...prevArr, 4]);
```