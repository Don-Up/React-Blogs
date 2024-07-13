# Data Transmission

In React applications, data transmission among components is a very common and essential operation. There are several primary ways of data transmission as follows:

1. Passing data downward using props.
2. Passing data upward using callback functions.
3. Passing data within the component tree using Context.
4. Using Redux or other state management libraries.
5. **使用 React Hooks 如 useContext 和 useReducer**
6. **使用 URL 参数和 React Router**

### 1. Passing data downward using props

Props is the primary way to pass data from parent components to child components. Child components access this data using `this.props` or parameters within functional components. 

#### 示例：

```jsx
// 父组件
class ParentComponent extends React.Component {
  state = {
    data: "Hello from Parent"
  };

  render() {
    return <ChildComponent data={this.state.data} />;
  }
}

// 子组件
const ChildComponent = (props) => {
  return <div>{props.data}</div>;
};
```

### 2. Passing data upward using callback functions.

Child components can pass data back to parent components by calling callback functions passed down from parent components.

#### 示例：

```jsx
// 父组件
class ParentComponent extends React.Component {
  state = {
    data: ""
  };

  handleDataChange = (newData) => {
    this.setState({ data: newData });
  };

  render() {
    return <ChildComponent onDataChange={this.handleDataChange} />;
  }
}

// 子组件
const ChildComponent = (props) => {
  const handleChange = (e) => {
    props.onDataChange(e.target.value);
  };

  return <input type="text" onChange={handleChange} />;
};
```

### 3. Passing data within the component tree using Context

React Context provides an approach to share data within the component tree without the need to manually pass props.

#### Cretae and use Context:

```jsx
const DataContext = React.createContext();

// 父组件
class ParentComponent extends React.Component {
  state = {
    data: "Hello from Context"
  };

  render() {
    return (
      <DataContext.Provider value={this.state.data}>
        <ChildComponent />
      </DataContext.Provider>
    );
  }
}

// 子组件
const ChildComponent = () => {
  return (
    <DataContext.Consumer>
      {data => <div>{data}</div>}
    </DataContext.Consumer>
  );
};
```

### 4. Using Redux or other state management libraries.

Redux is a popular state management library that suitable for complex applications. It uses global state storage and a dispatcher to manage and pass data.

#### Redux Example:

```jsx
// action.js
export const setData = data => ({
  type: "SET_DATA",
  payload: data
});

// reducer.js
const initialState = {
  data: ""
};

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case "SET_DATA":
      return { ...state, data: action.payload };
    default:
      return state;
  }
};

export default reducer;

// store.js
import { createStore } from "redux";
import reducer from "./reducer";

const store = createStore(reducer);

export default store;

// ParentComponent.js
import React from "react";
import { connect } from "react-redux";
import { setData } from "./action";

class ParentComponent extends React.Component {
  handleChange = (e) => {
    this.props.setData(e.target.value);
  };

  render() {
    return <input type="text" onChange={this.handleChange} />;
  }
}

const mapDispatchToProps = {
  setData
};

export default connect(null, mapDispatchToProps)(ParentComponent);

// ChildComponent.js
import React from "react";
import { connect } from "react-redux";

const ChildComponent = ({ data }) => {
  return <div>{data}</div>;
};

const mapStateToProps = (state) => ({
  data: state.data
});

export default connect(mapStateToProps)(ChildComponent);

// App.js
import React from "react";
import { Provider } from "react-redux";
import store from "./store";
import ParentComponent from "./ParentComponent";
import ChildComponent from "./ChildComponent";

const App = () => (
  <Provider store={store}>
    <ParentComponent />
    <ChildComponent />
  </Provider>
);

export default App;
```

### 5. 使用 React Hooks 如 useContext 和 useReducer

In functional components, it's a good practice to manage and pass data with `useContext` and `useReducer`

#### useContext 示例：

```jsx
const DataContext = React.createContext();

// 父组件
const ParentComponent = () => {
  const [data, setData] = React.useState("Hello from useContext");

  return (
    <DataContext.Provider value={data}>
      <ChildComponent />
    </DataContext.Provider>
  );
};

// 子组件
const ChildComponent = () => {
  const data = React.useContext(DataContext);
  return <div>{data}</div>;
};
```

#### useReducer 示例：

```jsx
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

const ParentComponent = () => {
  const [state, dispatch] = React.useReducer(reducer, initialState);

  return (
    <div>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <span>{state.count}</span>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
    </div>
  );
};
```

### 6. 使用 URL 参数和 React Router

In an application using React Router, you can pass data using URL parameters.

#### 示例：

```jsx
// App.js
import React from "react";
import { BrowserRouter as Router, Route, Link } from "react-router-dom";
import Home from "./Home";
import About from "./About";

const App = () => (
  <Router>
    <div>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about/123">About</Link>
          </li>
        </ul>
      </nav>

      <Route path="/" exact component={Home} />
      <Route path="/about/:id" component={About} />
    </div>
  </Router>
);

export default App;

// About.js
import React from "react";
import { useParams } from "react-router-dom";

const About = () => {
  let { id } = useParams();
  return <div>About ID: {id}</div>;
};

export default About;
```

### Summary

Data transmission among components is a core operation in React application development and can be implemented in multiple ways:

1. **通过 props 向下传递数据**：适用于简单的父子组件关系。
2. **通过回调函数向上传递数据**：适用于子组件需要将数据传回父组件的情况。
3. **使用 Context 在组件树中传递数据**：适用于跨越多个层级的组件数据共享。
4. **使用 Redux 或其他状态管理库**：适用于大型应用中复杂的全局状态管理。
5. **使用 React Hooks 如 useContext 和 useReducer**：适用于函数组件中的状态管理和数据传递。
6. **使用 URL 参数和 React Router**：适用于路由相关的数据传递。

Choosing a suitable way based on the specific application scenario can make the code more concise and easier to maintain.