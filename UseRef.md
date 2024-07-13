# UseRef

`useRef` is a React hook used to create a mutable and persistent reference object in functional components. It is usually used to directly access DOM elements, persist state, save instance variables, and control animations, among other things.

### 1. Basic Usage

Pass in an initial value and return an object, such as `xxRef`, which contains a unique property `current`.

```javascript
const xxRef = useRef(initialValue);
```

### 2. Access DOM elements

1. Declare a ref object:

   ```javascript
   const inputRef = useRef(null);
   ```

2. Specify the ref object:

   ```jsx
   <input ref={inputRef} />
   ```

3. Call methods of DOM elements:

   ```javascript
   inputRef.current.focus();
   ```

### 3. State Persistent

In asynchronous operations, `useRef` can persist state, enabling access to the latest state value.

```javascript
import React, { useRef, useState, useEffect } from 'react';

function Timer() {
  const [count, setCount] = useState(0);
  const countRef = useRef(count);

  useEffect(() => {
    countRef.current = count;
  }, [count]);

  const handleAlertClick = () => {
    setTimeout(() => {
      alert('Count is: ' + countRef.current);
    }, 3000);
  };

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={handleAlertClick}>Show Alert</button>
    </div>
  );
}

export default Timer;
```

### 4. Save instance variable

`useRef` can be used to save component instance variables, avoiding re-creation on each render.

```javascript
import React, { useRef } from 'react';

function RenderCounter() {
  const renderCount = useRef(0);
  
  renderCount.current += 1;

  return <div>Render count: {renderCount.current}</div>;
}

export default RenderCounter;
```

### 5. Control Animation

`useRef` can be used to store relevant state or references for animation, in order to control and access these states during animation.

```javascript
import React, { useRef, useEffect } from 'react';

function AnimatedComponent() {
  const animationRef = useRef(null);

  useEffect(() => {
    function startAnimation() {
      // start animation logic
    }

    animationRef.current = startAnimation();
    return () => {
      // clean up animation logic
    };
  }, []);

  return <div ref={animationRef}>Animated Content</div>;
}

export default AnimatedComponent;
```

### 6. Combine weith `forwardRef` 

`useRef` can be used with `forwardRef` to access the DOM elements or other references of child components from the parent component.

```javascript
import React, { useRef, forwardRef } from 'react';

const CustomInput = forwardRef((props, ref) => (
  <input ref={ref} {...props} />
));

function ParentComponent() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <CustomInput ref={inputRef} />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}

export default ParentComponent;
```

### Summary

useRef is a powerful tool used to create mutable and persistent reference objects within functional components. It is very useful in scenarios like handling direct DOM operations, state persistence, animation control, and combining with forwardRef. Understanding the usage of useRef can help in writing more efficient and robust React components.