# CSS

在 React 中使用 CSS 有多种方法，从传统的 CSS 文件到现代的 CSS-in-JS 解决方案。以下是总结在 React 中使用 CSS 的常见方法，尤其是使用原生 CSS 的方法：

### 1. 外部 CSS 文件

这是最常见的方法，将 CSS 样式定义在单独的 `.css` 文件中，然后在组件中引入。

#### 步骤

1. **创建 CSS 文件**：
   创建一个 CSS 文件，例如 `styles.css`：

   ```css
   .container {
     padding: 20px;
     background-color: #f4f4f4;
   }
   ```

2. **引入 CSS 文件**：
   在需要使用样式的 React 组件中引入该 CSS 文件：

   ```javascript
   import './styles.css';
   
   function App() {
     return <div className="container">Hello World</div>;
   }
   
   export default App;
   ```

### 2. 内联样式

在组件的 JSX 中直接使用 `style` 属性定义样式。内联样式是一个对象，键是驼峰式命名的 CSS 属性名，值是样式值。

#### 示例

```javascript
function App() {
  const divStyle = {
    padding: '20px',
    backgroundColor: '#f4f4f4'
  };

  return <div style={divStyle}>Hello World</div>;
}

export default App;
```

### 3. CSS 模块

CSS 模块允许你将 CSS 文件的样式作用域限定在一个特定的组件中，避免全局样式冲突。CSS 模块的文件名通常以 `.module.css` 结尾。

#### 步骤

1. **创建 CSS 模块文件**：
   创建一个 CSS 模块文件，例如 `styles.module.css`：

   ```css
   .container {
     padding: 20px;
     background-color: #f4f4f4;
   }
   ```

2. **引入 CSS 模块文件**：
   在组件中引入并使用该 CSS 模块：

   ```javascript
   import styles from './styles.module.css';
   
   function App() {
     return <div className={styles.container}>Hello World</div>;
   }
   
   export default App;
   ```

### 4. 使用 Sass/SCSS

Sass 是一种 CSS 预处理器，允许使用变量、嵌套规则、混合等功能来增强 CSS。你可以在 React 项目中使用 `.scss` 文件。

#### 步骤

1. **安装 Sass**：

   ```bash
   npm install sass
   ```

2. **创建 SCSS 文件**：
   创建一个 SCSS 文件，例如 `styles.scss`：

   ```scss
   $primary-color: #f4f4f4;
   
   .container {
     padding: 20px;
     background-color: $primary-color;
   }
   ```

3. **引入 SCSS 文件**：
   在组件中引入该 SCSS 文件：

   ```javascript
   import './styles.scss';
   
   function App() {
     return <div className="container">Hello World</div>;
   }
   
   export default App;
   ```

### 5. 动态类名

有时你需要根据组件的状态或属性动态地设置类名，`classnames` 库可以帮助你方便地处理这种情况。

#### 安装 `classnames`

```bash
npm install classnames
```

#### 使用 `classnames`

```javascript
import classNames from 'classnames';
import './styles.css';

function App({ isActive }) {
  const divClass = classNames('container', { active: isActive });

  return <div className={divClass}>Hello World</div>;
}

export default App;
```

### 6. 媒体查询和响应式设计

通过在 CSS 文件或 CSS 模块中使用媒体查询，您可以实现响应式设计。

```css
/* styles.css */
.container {
  padding: 20px;
  background-color: #f4f4f4;
}

@media (max-width: 600px) {
  .container {
    background-color: #ccc;
  }
}
```

在组件中引入：

```javascript
import './styles.css';

function App() {
  return <div className="container">Hello World</div>;
}

export default App;
```

### 总结

在 React 中使用 CSS 的方法多种多样，从传统的外部 CSS 文件到现代的 CSS-in-JS 解决方案，每种方法都有其独特的优势和适用场景。通过选择合适的方法，可以在项目中高效地管理和应用样式，提高代码的可维护性和可读性。

