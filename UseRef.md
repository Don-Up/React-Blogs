# UseRef

`useRef` 是一个用于在函数组件中创建一个可变的、持久的引用对象的 React Hook。它通常用于直接访问 DOM 元素、持久化状态、保存实例变量以及控制动画等。

### 1. 基本用法

1. 返回一个对象，例如 `xxRef`，唯一属性是 `current`。
2. 函数传入初始值。

```javascript
const xxRef = useRef(initialValue);
```

### 2. 访问 DOM 元素

1. 声明一个 ref 对象：

   ```javascript
   const inputRef = useRef(null);
   ```

2. 指定 ref 对象：

   ```jsx
   <input ref={inputRef} />
   ```

3. 调用 DOM 元素方法：

   ```javascript
   inputRef.current.focus();
   ```

### 3. 持久化状态

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

### 4. 保存实例变量

`useRef` 可以用来保存组件实例的变量，避免在每次渲染时重新创建。

```javascript
import React, { useRef } from 'react';

function RenderCounter() {
  const renderCount = useRef(0);
  
  renderCount.current += 1;

  return <div>Render count: {renderCount.current}</div>;
}

export default RenderCounter;
```

### 5. 控制动画

`useRef` can be used to store relevant state or references for animation, in order to control and access these states during animation.

```javascript
import React, { useRef, useEffect } from 'react';

function AnimatedComponent() {
  const animationRef = useRef(null);

  useEffect(() => {
    function startAnimation() {
      // 开始动画逻辑
    }

    animationRef.current = startAnimation();
    return () => {
      // 清理动画逻辑
    };
  }, []);

  return <div ref={animationRef}>Animated Content</div>;
}

export default AnimatedComponent;
```

### 6. 与 `forwardRef` 结合

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