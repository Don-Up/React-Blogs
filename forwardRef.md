# forwardRef

`forwardRef` is a utility provided by React that allows you to pass a ref through a component to one of its children. 

## Why `forwardRef` is needed?

In functional components, parent components cannot pass a `ref` to child components directly, because `ref` is specifically designed to be used with DOM elements or class components. By default, when you assign a `ref` to a functional component, React doesn't know how to handle it since functional components do not have instances.

## Generic Types and parameters

1. **Generic Type 1**: The first generic type of `forwardRef` corresponds to the generic type in `useRef<>`. In general, how you define the generic type depends on how the parent component operates on the child component. For example, if you want to focus the child's input, you can pass in `HTMLInputElement`. If you want to expose the child's custom methods to the parent, you can pass in a custom interface consisting of method signatures.
2. **Generic Type 2**: The second generic type of `forwardRef` specifies the parameter list, depending on which parameters the child component wants to receive from the parent.
3. **Callback Parameters**: The first parameter is a destructured object of the second generic type. The second parameter is a `ref`.

## useImperativeHandle

As mentioned before, if you want to expose custom methods of the child component to the parent, you can pass a custom interface consisting of method signatures into the first generic type of `forwardRef`. So, how do you implement these method signatures? You can use `useImperativeHandle` and pass in a `ref` along with a callback that returns an object containing the methods.

### Scenarios for Using `forwardRef`

1. **Accessing Child Component's DOM Node**:
   - When you need to access the DOM node of a child component from a parent component, especially for manipulating the DOM directly, applying focus, or integrating with third-party libraries.

2. **Higher-Order Components (HOCs)**:
   - When creating HOCs that need to forward refs to wrapped components. This ensures that refs are properly forwarded to the underlying DOM elements or components.

3. **Reusable Components**:
   - When building reusable components like custom input fields, buttons, or modals that require access to the DOM node for focus management, animations, or other DOM manipulations.

### Example: Accessing Child Component's DOM Node

Here's an example to demonstrate how `forwardRef` can be used to forward a ref to a DOM element within a child component.

```typescript
import React, { useRef, forwardRef, useImperativeHandle } from 'react';

// Child component using forwardRef
const CustomInput = forwardRef<HTMLInputElement, { label: string }>(({ label }, ref) => {
    return (
        <div>
            <label>{label}</label>
            <input ref={ref} type="text" />
        </div>
    );
});

// Parent component
const ParentComponent: React.FC = () => {
    const inputRef = useRef<HTMLInputElement>(null);

    const focusInput = () => {
        if (inputRef.current) {
            inputRef.current.focus();
        }
    };

    return (
        <div>
            <CustomInput label="Name:" ref={inputRef} />
            <button onClick={focusInput}>Focus Input</button>
        </div>
    );
};

export default ParentComponent;
```

### Example: Using `forwardRef` with `useImperativeHandle`

You can also use `forwardRef` in combination with `useImperativeHandle` to customize the instance value that is exposed to parent components when using refs.

```typescript
import React, { useRef, forwardRef, useImperativeHandle } from 'react';

// Child component using forwardRef and useImperativeHandle
const CustomInput = forwardRef((props, ref) => {
    const inputRef = useRef<HTMLInputElement>(null);

    useImperativeHandle(ref, () => ({
        focus: () => {
            if (inputRef.current) {
                inputRef.current.focus();
            }
        },
        clear: () => {
            if (inputRef.current) {
                inputRef.current.value = '';
            }
        }
    }));

    return (
        <div>
            <input ref={inputRef} type="text" />
        </div>
    );
});

// Parent component
const ParentComponent: React.FC = () => {
    const customInputRef = useRef<{ focus: () => void; clear: () => void }>(null);

    return (
        <div>
            <CustomInput ref={customInputRef} />
            <button onClick={() => customInputRef.current?.focus()}>Focus Input</button>
            <button onClick={() => customInputRef.current?.clear()}>Clear Input</button>
        </div>
    );
};

export default ParentComponent;
```

### Summary

`forwardRef` is a powerful tool for passing refs through component trees, making it easier to interact with child components' DOM nodes or instances. It is especially useful in scenarios involving HOCs, reusable components, and any situation where direct DOM manipulation or focus management is necessary. By using `forwardRef` and `useImperativeHandle`, you can create flexible and reusable components that provide a clean interface for interacting with their internal state and DOM elements.