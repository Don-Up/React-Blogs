# Class components

React class components are a way to define components in React. They provide hooks and lifecycle methods to better control the behavior of components. Using TypeScript can enhance the type safety and maintainability of the code. The following is a summary of common usage of React class components.

## Class components review

1. Class components need to inherit from the Component class. The class needs to specify two generic types: the first is `Props`, which represents the component's properties, and the second is `State`, which represents the component's state. Of course, you can also specify one of them or even none. If neither is specified, you can pass an empty object `{}` to indicate it. If it is the state, you can also omit it directly.

   ```tsx
   // Case 1: Specifying both Props and State
   interface MyProps {
     message: string;
   }
   
   interface MyState {
     count: number;
   }
   
   class MyComponent1 extends Component<MyProps, MyState> {
     state: MyState = {
       count: 0
     };
   
     render() {
       return (
         <div>
           <p>{this.props.message}</p>
           <p>Count: {this.state.count}</p>
         </div>
       );
     }
   }
   
   // Case 2: Specifying only Props
   class MyComponent2 extends Component<MyProps> {
     render() {
       return <p>{this.props.message}</p>;
     }
   }
   
   // Case 3: Specifying only State
   class MyComponent3 extends Component<{}, MyState> {
     state: MyState = {
       count: 0
     };
   
     render() {
       return <p>Count: {this.state.count}</p>;
     }
   }
   
   // Case 4: Specifying neither Props nor State
   class MyComponent4 extends Component {
     render() {
       return <p>Hello, world!</p>;
     }
   }
   
   // Case 5: Specifying empty objects for both Props and State
   class MyComponent5 extends Component<{}, {}> {
     render() {
       return <p>Hello, world!</p>;
     }
   }
   
   // Case 6: Omitting State (similar to Case 2, shown for completeness)
   class MyComponent6 extends Component<MyProps> {
     render() {
       return <p>{this.props.message}</p>;
     }
   }
   ```

2. For the initialization of state, it's suggested to use class field syntax. The format is as follows:

   ```tsx
   state: XxxState = {
       属性名:属性值,
       ...
   }
   ```

3. You can also initialize state in the constructor function：

   ```tsx
   constructor(props:XxxProps){
       super(props)
       this.state = {属性名:属性值, ...}
   }
   ```

4. Update state, call this.setState(new state object)：

   ```tsx
   // Note: The update of setState is partial, so if you don't need to add or remove properties, you don't need to use the spread operator; just pass in the properties that need to be updated.
   this.setState({ count: this.state.count + 1 });
   this.setState(prevState => (新状态对象))
   ```

5. 使用props，使用this.props.xxx来使用props的属性。注意不能在当前组件中直接修改props中的属性。

6. render方法，返回JSX。

7. 组件声明周期方法，最主要的三个：componentDidMount(挂载时)、componentDidUpdate(更新时)、 componentWillUnmount(卸载时)。

8. 事件处理：同样适用类字段语法，格式如下：

   ```tsx
   // 通过this.handleXxx调用
   handleXxx:()=>{}
   ```

9. 条件渲染，在JSX中，主要通过三目运算符来实现条件渲染。

### 基本用法

#### 定义类组件

在 TypeScript 中定义一个类组件，需要继承自 `React.Component` 并指定 props 和 state 的类型：

```tsx
import React, { Component } from 'react';

interface Props {
  name: string;
}

interface State {
  count: number;
}

class MyComponent extends Component<Props, State> {
  state: State = {
    count: 0,
  };

  render() {
    return (
      <div>
        <h1>Hello, {this.props.name}!</h1>
        <p>Count: {this.state.count}</p>
      </div>
    );
  }
}

export default MyComponent;
```

### 组件生命周期方法

React class components provide a rich set of lifecycle methods that can execute code at different stages of the component's lifecycle.

#### 常用生命周期方法

1. **`componentDidMount`**：组件挂载后调用，适合进行数据获取等操作。
2. **`componentDidUpdate`**：组件更新后调用，适合进行依赖于更新后的操作。
3. **`componentWillUnmount`**：组件卸载前调用，适合进行清理操作。

```typescript
class MyComponent extends Component<Props, State> {
  componentDidMount() {
    console.log('Component did mount');
  }

  componentDidUpdate(prevProps: Props, prevState: State) {
    if (prevState.count !== this.state.count) {
      console.log('Component did update');
    }
  }

  componentWillUnmount() {
    console.log('Component will unmount');
  }

  render() {
    return (
      <div>
        <h1>Hello, {this.props.name}!</h1>
        <p>Count: {this.state.count}</p>
      </div>
    );
  }
}
```

### Event Handling

When defining an event handling function within class components, we usually need to bind `this`, but we can automatically bind it using an arrow function.

```typescript
class MyComponent extends Component<Props, State> {
  state: State = {
    count: 0,
  };

  handleIncrement = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <h1>Hello, {this.props.name}!</h1>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleIncrement}>Increment</button>
      </div>
    );
  }
}
```

### Conditional Rendering

You can use either conditional operator or logical operator to perform conditional rendering.

```typescript
class MyComponent extends Component<Props, State> {
  state: State = {
    count: 0,
  };

  render() {
    const { count } = this.state;

    return (
      <div>
        <h1>Hello, {this.props.name}!</h1>
        {count > 0 ? <p>Count: {count}</p> : <p>No count yet</p>}
        <button onClick={() => this.setState({ count: count + 1 })}>
          Increment
        </button>
      </div>
    );
  }
}
```

### State Management

In class components, use the `setState` method to update the component's state. `setState` can take either an object or a function that returns an object.

```typescript
class MyComponent extends Component<Props, State> {
  state: State = {
    count: 0,
  };

  increment = () => {
    this.setState(prevState => ({ count: prevState.count + 1 }));
  };

  render() {
    return (
      <div>
        <h1>Hello, {this.props.name}!</h1>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}
```

### Type Checking

Using TypeScript ensures the type correctness of a component's props and state, thereby improving code safety and maintainability.

```typescript
interface Props {
  name: string;
  age?: number; // 可选属性
}

interface State {
  count: number;
}

class MyComponent extends Component<Props, State> {
  static defaultProps = {
    age: 30, // 默认值
  };

  state: State = {
    count: 0,
  };

  render() {
    return (
      <div>
        <h1>Hello, {this.props.name}!</h1>
        <p>Age: {this.props.age}</p>
        <p>Count: {this.state.count}</p>
      </div>
    );
  }
}
```

### Advanced Usage

#### Use Refs

Refs provide a way to access DOM nodes or React elements.

```typescript
class MyComponent extends Component<Props, State> {
  private inputRef = React.createRef<HTMLInputElement>();

  focusInput = () => {
    if (this.inputRef.current) {
      this.inputRef.current.focus();
    }
  };

  render() {
    return (
      <div>
        <input ref={this.inputRef} type="text" />
        <button onClick={this.focusInput}>Focus Input</button>
      </div>
    );
  }
}
```

#### Context API

Use the Context API to pass data within the component tree without the need to pass props layer-by-layer.

```typescript
const MyContext = React.createContext<{ name: string }>({ name: 'Default' });

class MyComponent extends Component<Props, State> {
  render() {
    return (
      <MyContext.Provider value={{ name: 'John' }}>
        <MyContext.Consumer>
          {context => <h1>Hello, {context.name}!</h1>}
        </MyContext.Consumer>
      </MyContext.Provider>
    );
  }
}
```

### Sum-up

React class components provide powerful functionality and flexibility. Using TypeScript can significantly enhance code type safety and maintainability. By mastering the basic usage of class components, their lifecycle methods, event handling, conditional rendering, state management, type checking, and advanced usage (such as using Refs and the Context API), you can better develop complex and high-performance React applications.

For more information and detailed examples, please refer to:

- [React Official Documentation](https://reactjs.org/docs/react-component.html)
- [TypeScript Official Documentation](https://www.typescriptlang.org/docs/)

These resources provide comprehensive guides and best practices, helping developers better understand and use React class components and TypeScript.



