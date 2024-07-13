# StyledComponent

Styled Components is a library for managing styles using JavaScript and CSS. It allows you to directly write styles in React components, supporting advanced features like CSS variables, nesting, and dynamic styling. Its main advantages include local scope, dynamic styling and better maintainability.

### **Installation**

> 1. npm install styled-components
> 2. yarn add styled-components

### Create and use styled components

1. Use `styled.xxx` to return a styled component, such as `styled.button` returning a Button.
   1. Define CSS rules within backticks ``.
   2. Define pseudo-classes using  `&:xxx` within backticks.
2. Wrap components that need to apply styles using `<Button></Button>` in JSX.

```jsx
const Button = styled.button`
  background-color: #4CAF50; /* Green background */
  &:hover {
    background-color: #45a049; /* Darker green on hover */
  }
`;

const App = () => {
  return (
    <div>
      <Button>Click Me</Button>
    </div>
  );
};
```

### Dynamic styles

Dynamically change styles by combining `props` passing, `${}`, and `props =>`.

```jsx
const Button = styled.button<{primary?: boolean}>`
  background: ${props => props.primary ? 'palevioletred' : 'white'};
  
  &:hover {
    background: ${props => props.primary ? 'darkred' : 'lightgray'};
  }
`;

const App = () => {
  return (
    <div>
      <Button primary>Primary</Button>
    </div>
  );
};
```

### Style Nesting

```jsx
const Card = styled.div`
  padding: 1em;
  background: papayawhip;

  h2 {
    color: palevioletred;
  }
`;

function App() {
  return (
    <Card>
      <h2>Title</h2>
      <p>Content</p>
    </Card>
  );
}
```

### Style Inheritance

```jsx
const Button = styled.button`
  background: palevioletred;
  color: white;
`;
// Use style() to wrap the inherited component.
const PrimaryButton = styled(Button)`
  background: darkviolet;
`;

function App() {
  return <PrimaryButton>Click me</PrimaryButton>;
}
```

### Use theme

```jsx
// define a theme
const theme = {
  colors: {
    primary: 'palevioletred',
    secondary: 'papayawhip'
  }
};

const Button = styled.button`
  // Set the background to the color defined in the theme.
  background: ${props => props.theme.colors.primary};
`;

function App() {
  return (
     // Use the ThemeProvider component and pass in the theme.
    <ThemeProvider theme={theme}>
      <Button>Click me</Button>
    </ThemeProvider>
  );
}
```

### createGlobalStyle

Because `GlobalStyle` changes the `body` style, all content in the entire application will be affected, including all same-level components and their child components.

```jsx
const GlobalStyle = createGlobalStyle`
  body {
    margin: 0;
    padding: 0;
    font-family: sans-serif;
    background: papayawhip;
  }
`;

function App() {
  return (
    <>   
      <GlobalStyle />
      <Button>Click me</Button>
    </>
  );
}

```

### Media queries

```jsx
const Container = styled.div`
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  
  @media (max-width: 768px) {
    max-width: 100%;
  }
`;
```

### Use Ref to get the component reference

```javascript
const Input = styled.input`
  padding: 0.5em;
  margin: 0.5em;
  color: palevioletred;
  background: papayawhip;
  border: none;
  border-radius: 3px;
`;

function App() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return <Input ref={inputRef} placeholder="Focus me on mount" />;
}
```

### Animation

```javascript
// First use keyframes to define an animation
const rotate = keyframes`
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
`;

// Use ${} to introduce the animation in CSS rules
const RotatingDiv = styled.div`
  display: inline-block;
  animation: ${rotate} 2s linear infinite;
`;

function App() {
  return <RotatingDiv>🔄</RotatingDiv>;
}
```



