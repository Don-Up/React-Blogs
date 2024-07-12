# StyledComponent

Styled Components 是一种使用 JavaScript 和 CSS 进行样式管理的库，它允许你在 React 组件中直接编写样式，同时支持 CSS 变量、嵌套和动态样式等高级功能。它的主要优点包括样式的局部作用域、动态样式和更好的可维护性。

1. **安装**。

   1. npm install styled-components。
   2. yarn add styled-components。

2. **创建和使用样式组件**。

   1. 使用styled.xxx``返回一个样式组件，<small>例如styled.button返回Button</small>。
      1. 在``内部定义CSS规则。
      2. 在``内部可以通过&:xxx语法定义伪类。
   2. 在JSX中使用`<Button></Button>`包裹需要应用样式的组件。

3. **动态样式。**

   1. 通过传递props搭配${}和props=>语法来动态改变样式。
   2. `styled.button<{primary?:boolean}>`
   3. ` <Button primary>Primary</Button>`
   4. `background: ${props => props.primary ? 'palevioletred' : 'white'};`

4. **嵌套样式**(针对组件内部的元素进行样式定义)。

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

5. **继承样式**(扩展现有组件来创建具有附加样式的组件)

   ```jsx
   const Button = styled.button`
     background: palevioletred;
     color: white;
   `;
   // 使用style()包括被继承的组件。
   const PrimaryButton = styled(Button)`
     background: darkviolet;
   `;
   
   function App() {
     return <PrimaryButton>Click me</PrimaryButton>;
   }
   ```

6. **使用主题**。

   ```jsx
   // 定义主题
   const theme = {
     colors: {
       primary: 'palevioletred',
       secondary: 'papayawhip'
     }
   };
   
   const Button = styled.button`
     // 设置为主题中定义的颜色
     background: ${props => props.theme.colors.primary};
     color: white;
   `;
   
   function App() {
     return (
        // 使用ThemeProvider组件 
       <ThemeProvider theme={theme}>
         <Button>Click me</Button>
       </ThemeProvider>
     );
   }
   ```

7. **全局样式**(createGlobalStyle)

   由于 `GlobalStyle` 修改了 `body` 元素的样式，因此整个应用程序的所有内容都会受到影响。这包括与 `GlobalStyle` 同级的 `Button` 组件及其所有子组件。

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

8. **媒体查询**(语法与在css中一致)

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

9. **使用 Ref获取组件引用**

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

10. **动画**(keyframes)

    ```javascript
    // 先使用keyframes定义动画
    const rotate = keyframes`
      from {
        transform: rotate(0deg);
      }
      to {
        transform: rotate(360deg);
      }
    `;
    
    // 在组件规则中使用${}引入动画
    const RotatingDiv = styled.div`
      display: inline-block;
      animation: ${rotate} 2s linear infinite;
    `;
    
    function App() {
      return <RotatingDiv>🔄</RotatingDiv>;
    }
    ```



