# HOC

A Higher-Order Component (HOC) is a design pattern in React for reusing component logic. Essentially, it's a function that takes a component as an argument and returns a new component. HOCs do not modify the original component; instead, they extend its functionality by wrapping it.

### Summary of Implementing a Higher-Order Component

1. **Define the Higher-Order Component Function**:
    - Use a generic `T` to represent the props type of the component being passed in.
    - Accept a component as an argument and return a new component.

2. **Implement Additional Functionality in the Returned Component**:
    - Define state, lifecycle methods, context, etc., in the new component.
    - Use `useEffect` to add side effect logic such as data fetching or timers.

3. **Pass the Received Props to the Wrapped Component**:
    - Define the props type of the new component using `props: T`.
    - Pass these props to the wrapped component to ensure it renders correctly.

4. **Return the New Component**:
    - The new component can render additional content (like a loading indicator, error boundary, etc.) as needed, and then render the wrapped component.

### Code Example

Here is a simple example of a Higher-Order Component that adds a loading state to the wrapped component:

```typescript
import React, { useState, useEffect } from 'react';

function withLoading<T>(WrappedComponent: React.ComponentType<T>) {
    return (props: T) => {
        const [isLoading, setIsLoading] = useState(true);

        useEffect(() => {
            const timer = setTimeout(() => {
                setIsLoading(false);
            }, 1000);

            return () => clearTimeout(timer);
        }, []);

        if (isLoading) {
            return <div>Loading...</div>;
        }

        // @ts-ignore
        return <WrappedComponent {...props} />;
    };
}

export default withLoading;
```

```tsx
import React from "react";
import withLoading from "./withLoading";

const HOCPage: React.FC = () => {
    return (<div><h1>HOCPage</h1></div>)
}

const HOCLoadingPage = withLoading(HOCPage)

export default HOCLoadingPage
```

### Key Points Summary

1. **Define Generic Type**:
   ```typescript
   function withLoading<T>(WrappedComponent: React.ComponentType<T>) { ... }
   ```

2. **Return a New Functional Component**:
   ```typescript
   return (props: T) => { ... }
   ```

3. **Add State and Side Effects**:
   ```typescript
   const [isLoading, setIsLoading] = useState(true);
   
   useEffect(() => {
       const timer = setTimeout(() => {
           setIsLoading(false);
       }, 1000);
   
       return () => clearTimeout(timer);
   }, []);
   ```

4. **Conditional Rendering or Wrapping the Wrapped Component**:
   ```typescript
   if (isLoading) {
       return <div>Loading...</div>;
   }
   
   return <WrappedComponent {...props} />;
   ```

In this way, you can create a reusable Higher-Order Component to extend the functionality of other components without modifying the original component's implementation.