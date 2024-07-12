# 动画和过渡

## 原生CSS

在原生 CSS 中实现动画和过渡（transition）的效果是创建动态和互动网页的重要技术。以下是全面总结如何在原生 CSS 中实现动画和过渡的方法：

### 1. CSS 过渡（Transitions）

过渡用于在元素从一种状态变为另一种状态时逐步应用效果。

#### 基本语法

```css
.element {
  transition: property duration timing-function delay;
}
```

#### 示例

```css
button {
    background-color: blue;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.3s;
}

button:hover {
    background-color: darkblue;
    transform: scale(1.1);
}
```

### 2. CSS 动画（Animations）

动画用于创建更复杂的效果，可以控制更细致的动画步骤。

#### 基本语法

定义动画：

```css
@keyframes animationName {
  from {
    /* 初始状态 */
  }
  to {
    /* 结束状态 */
  }
  /* 或者使用多个中间状态 */
  0% {
    /* 起始状态 */
  }
  50% {
    /* 中间状态 */
  }
  100% {
    /* 结束状态 */
  }
}
```

将动画应用于元素：

```css
.element {
  animation: animationName duration timing-function delay iteration-count direction fill-mode;
}
```

#### 示例

```css
@keyframes slide {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(100px);
  }
}

.box {
  width: 100px;
  height: 100px;
  background-color: blue;
  animation: slide 2s ease-in-out infinite;
}
```

### 3. 过渡属性详解

- **property**: 需要过渡的 CSS 属性（如 `background-color`, `width`, `height`）。
- **duration**: 过渡效果的持续时间（如 `0.5s` 或 `200ms`）。
- **timing-function**: 过渡效果的速度曲线（如 `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out`）。
- **delay**: 过渡效果开始前的延迟时间（如 `0s`, `1s`）。

### 4. 动画属性详解

- **animation-name**: 关键帧动画的名称。
- **duration**: 动画的持续时间（如 `2s`, `3s`）。
- **timing-function**: 动画的速度曲线（如 `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out`）。
- **delay**: 动画开始前的延迟时间（如 `0s`, `1s`）。
- **iteration-count**: 动画的循环次数（如 `1`, `infinite`）。
- **direction**: 动画的方向（如 `normal`, `reverse`, `alternate`, `alternate-reverse`）。
- **fill-mode**: 动画结束后的状态（如 `none`, `forwards`, `backwards`, `both`）。

### 5. 常见开发场景

#### 悬停效果

在用户悬停元素时应用过渡效果：

```css
.button {
  background-color: blue;
  transition: background-color 0.3s;
}

.button:hover {
  background-color: green;
}
```

#### 加载动画

在页面加载时显示动画效果：

```css
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.loader {
  width: 50px;
  height: 50px;
  background-color: red;
  animation: fadeIn 2s ease-in-out;
}
```

#### 滚动动画

在元素进入视口时触发动画：

```css
@keyframes slideIn {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
  }
}

.scroll-element {
  animation: slideIn 1s ease-out;
}
```

#### 响应式动画

根据屏幕大小调整动画效果：

```css
@media (max-width: 600px) {
  .box {
    animation: slide 1s ease-in-out infinite;
  }
}

@media (min-width: 601px) {
  .box {
    animation: slide 2s ease-in-out infinite;
  }
}
```

### 小结

通过过渡（transitions）和动画（animations），可以在网页中创建平滑和吸引人的视觉效果。过渡适合简单的状态变化，而动画则用于复杂的多步骤效果。掌握这些技术，可以显著提升用户体验和界面交互性。



# AnimateCSS

Animate.css 是一个流行的 CSS 库，它提供了一组预定义的动画效果，便于开发者快速在网页中实现动画。以下是 Animate.css 的常见用法总结，包括如何引入和使用这些动画效果。

### 安装和引入

#### 通过 CDN 引入

可以直接在 HTML 文件中通过 CDN 引入 Animate.css：

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"/>
```

#### 通过 npm 安装

也可以通过 npm 安装 Animate.css：

```bash
npm install animate.css --save
```

然后在项目中引入：

```javascript
import 'animate.css';
```

### 基本用法

在需要动画的元素上添加 `animate__animated` 类和具体的动画类名即可。例如：

```html
<div class="animate__animated animate__bounce">
  这是一个有动画的元素
</div>
```

### 动画类名

Animate.css 提供了多种动画效果，以下是一些常见的动画类名：

- **进入/退出动画**：
  - `animate__bounce`
  - `animate__flash`
  - `animate__pulse`
  - `animate__rubberBand`
  - `animate__shakeX`
  - `animate__shakeY`
  - `animate__headShake`
  - `animate__swing`
  - `animate__tada`
  - `animate__wobble`
  - `animate__jello`
  - `animate__heartBeat`

- **翻转动画**：
  - `animate__flip`
  - `animate__flipInX`
  - `animate__flipInY`
  - `animate__flipOutX`
  - `animate__flipOutY`

- **渐变动画**：
  - `animate__fadeIn`
  - `animate__fadeInDown`
  - `animate__fadeInDownBig`
  - `animate__fadeInLeft`
  - `animate__fadeInLeftBig`
  - `animate__fadeInRight`
  - `animate__fadeInRightBig`
  - `animate__fadeInUp`
  - `animate__fadeInUpBig`
  - `animate__fadeOut`
  - `animate__fadeOutDown`
  - `animate__fadeOutDownBig`
  - `animate__fadeOutLeft`
  - `animate__fadeOutLeftBig`
  - `animate__fadeOutRight`
  - `animate__fadeOutRightBig`
  - `animate__fadeOutUp`
  - `animate__fadeOutUpBig`

- **滑动动画**：
  - `animate__slideInDown`
  - `animate__slideInLeft`
  - `animate__slideInRight`
  - `animate__slideInUp`
  - `animate__slideOutDown`
  - `animate__slideOutLeft`
  - `animate__slideOutRight`
  - `animate__slideOutUp`

- **缩放动画**：
  - `animate__zoomIn`
  - `animate__zoomInDown`
  - `animate__zoomInLeft`
  - `animate__zoomInRight`
  - `animate__zoomInUp`
  - `animate__zoomOut`
  - `animate__zoomOutDown`
  - `animate__zoomOutLeft`
  - `animate__zoomOutRight`
  - `animate__zoomOutUp`

- **旋转动画**：
  - `animate__rotateIn`
  - `animate__rotateInDownLeft`
  - `animate__rotateInDownRight`
  - `animate__rotateInUpLeft`
  - `animate__rotateInUpRight`
  - `animate__rotateOut`
  - `animate__rotateOutDownLeft`
  - `animate__rotateOutDownRight`
  - `animate__rotateOutUpLeft`
  - `animate__rotateOutUpRight`

### 控制动画重复次数

可以通过 `animate__repeat-{n}` 类来控制动画的重复次数，例如：

```html
<div class="animate__animated animate__bounce animate__repeat-2">
  这是一个重复两次的动画
</div>
```

### 延迟和持续时间

可以通过自定义 CSS 来控制动画的延迟和持续时间：

```html
<div class="animate__animated animate__bounce" style="animation-delay: 2s; animation-duration: 3s;">
  这是一个有延迟和自定义持续时间的动画
</div>
```

### 使用 JavaScript 控制动画

可以通过 JavaScript 动态地添加和移除类来控制动画：

```javascript
const element = document.querySelector('.my-element');
element.classList.add('animate__animated', 'animate__bounce');

// 动画结束后移除类
element.addEventListener('animationend', () => {
  element.classList.remove('animate__animated', 'animate__bounce');
});
```

### 实用技巧

1. **结合过渡效果**：可以将 Animate.css 与 CSS 过渡效果结合使用，创建更复杂的动画效果。
2. **响应式设计**：确保动画在不同屏幕尺寸下表现良好，可以通过媒体查询自定义动画。
3. **性能优化**：对于性能敏感的应用，尽量减少动画的使用或使用硬件加速的动画效果。

### 资源

- 官方文档和示例：[Animate.css](https://animate.style/)
- GitHub 仓库：[Animate.css on GitHub](https://github.com/animate-css/animate.css)

通过掌握这些常见用法和技巧，可以充分利用 Animate.css 在网页中创建生动和互动的动画效果。



# react-transition-group

`react-transition-group` 是一个用于在 React 应用中实现动画和过渡效果的库。它提供了一组组件和工具，方便地管理组件在进入和离开视图时的过渡效果。以下是 `react-transition-group` 的常见用法总结：

### 安装

首先，安装 `react-transition-group`：

```bash
npm install react-transition-group
```

### 基本组件

#### Transition

`Transition` 组件是所有过渡组件的基础，它不会在组件上应用任何样式，而是用来管理组件的进入和离开状态。

```jsx
import { Transition } from 'react-transition-group';

const duration = 300;

const defaultStyle = {
  transition: `opacity ${duration}ms ease-in-out`,
  opacity: 0,
};

const transitionStyles = {
  entering: { opacity: 1 },
  entered: { opacity: 1 },
  exiting: { opacity: 0 },
  exited: { opacity: 0 },
};

const Fade = ({ in: inProp }) => (
  <Transition in={inProp} timeout={duration}>
    {state => (
      <div style={{
        ...defaultStyle,
        ...transitionStyles[state]
      }}>
        I'm a fade Transition!
      </div>
    )}
  </Transition>
);
```

#### CSSTransition

`CSSTransition` 组件会在元素进入和离开时应用 CSS 类名。

```jsx
import { CSSTransition } from 'react-transition-group';
import './styles.css'; // 确保你定义了相应的 CSS 类名

const Fade = ({ in: inProp }) => (
  <CSSTransition in={inProp} timeout={300} classNames="fade">
    <div>
      I'm a fade CSSTransition!
    </div>
  </CSSTransition>
);
```

`styles.css`：

```css
.fade-enter {
  opacity: 0;
}
.fade-enter-active {
  opacity: 1;
  transition: opacity 300ms;
}
.fade-exit {
  opacity: 1;
}
.fade-exit-active {
  opacity: 0;
  transition: opacity 300ms;
}
```

#### TransitionGroup

`TransitionGroup` 组件用于管理一组 `Transition` 或 `CSSTransition` 组件，可以在组件添加或删除时应用动画效果。

```jsx
import { TransitionGroup, CSSTransition } from 'react-transition-group';

const List = ({ items }) => (
  <TransitionGroup>
    {items.map(item => (
      <CSSTransition key={item} timeout={500} classNames="item">
        <div>
          {item}
        </div>
      </CSSTransition>
    ))}
  </TransitionGroup>
);
```

`styles.css`：

```css
.item-enter {
  opacity: 0;
  transform: translateY(-20px);
}
.item-enter-active {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 500ms, transform 500ms;
}
.item-exit {
  opacity: 1;
  transform: translateY(0);
}
.item-exit-active {
  opacity: 0;
  transform: translateY(-20px);
  transition: opacity 500ms, transform 500ms;
}
```

### 高级用法

#### 使用状态机

通过 `Transition` 的 `state` 属性可以实现复杂的状态管理。

```javascript
const Fade = ({ in: inProp }) => (
  <Transition in={inProp} timeout={300}>
    {state => {
      switch(state) {
        case 'entering':
          // entering 状态
          break;
        case 'entered':
          // entered 状态
          break;
        case 'exiting':
          // exiting 状态
          break;
        case 'exited':
          // exited 状态
          break;
        default:
          return null;
      }
    }}
  </Transition>
);
```

#### 控制动画生命周期

使用 `Transition` 的钩子函数可以在动画生命周期的不同阶段执行代码。

```javascript
<Transition
  in={inProp}
  timeout={300}
  onEnter={() => console.log('Entering')}
  onEntered={() => console.log('Entered')}
  onExit={() => console.log('Exiting')}
  onExited={() => console.log('Exited')}
>
  {state => (
    <div style={{
      ...defaultStyle,
      ...transitionStyles[state]
    }}>
      I'm a transition with lifecycle hooks!
    </div>
  )}
</Transition>
```

### 小结

`react-transition-group` 是一个强大的动画库，通过其提供的 `Transition`、`CSSTransition` 和 `TransitionGroup` 组件，可以在 React 应用中轻松实现复杂的过渡效果。通过掌握其基本用法和高级技巧，开发者可以创建更加动态和互动的用户界面。