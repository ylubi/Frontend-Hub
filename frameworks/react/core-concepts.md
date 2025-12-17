# React 核心概念

## 目录

- [什么是 React](#什么是-react)
- [React 的特点](#react-的特点)
- [React 核心概念](#react-核心概念)
  - [JSX](#jsx)
  - [组件](#组件)
  - [Props](#props)
  - [State](#state)
  - [生命周期](#生命周期)
  - [事件处理](#事件处理)
- [React Hooks](#react-hooks)
  - [useState](#usestate)
  - [useEffect](#useeffect)
  - [useContext](#usecontext)
  - [useReducer](#usereducer)
  - [useCallback](#usecallback)
  - [useMemo](#usememo)
  - [useRef](#useref)
  - [自定义 Hooks](#自定义-hooks)
- [React 生态](#react-生态)
  - [React Router](#react-router)
  - [状态管理](#状态管理)
  - [数据获取](#数据获取)
  - [UI 组件库](#ui-组件库)
- [React 最佳实践](#react-最佳实践)
- [参考资源](#参考资源)

## 什么是 React

React 是一个用于构建用户界面的 JavaScript 库，由 Facebook（现 Meta）开发并开源。它允许开发者创建可复用的 UI 组件，并通过组件化的方式构建复杂的用户界面。

React 采用声明式编程模型，开发者只需要描述 UI 应该是什么样子，而不需要关心如何更新 DOM。React 会自动处理 DOM 的更新，使开发者能够专注于业务逻辑。

## React 的特点

1. **组件化**：将 UI 拆分为独立的、可复用的组件
2. **声明式**：描述 UI 应该是什么样子，而不是如何更新
3. **虚拟 DOM**：通过虚拟 DOM 提高性能，减少直接操作真实 DOM 的次数
4. **单向数据流**：数据从父组件流向子组件，便于追踪和调试
5. **JSX**：JavaScript 的语法扩展，允许在 JavaScript 中编写 HTML
6. **跨平台**：可以用于构建 Web、移动应用（React Native）和桌面应用（Electron）
7. **丰富的生态系统**：拥有大量的第三方库和工具

## React 核心概念

### JSX

JSX（JavaScript XML）是 JavaScript 的语法扩展，允许在 JavaScript 中编写类似 HTML 的代码。JSX 使得开发者可以更直观地描述 UI 结构。

```jsx
const element = <h1>Hello, World!</h1>;
```

JSX 会被 Babel 等工具编译为普通的 JavaScript 函数调用：

```javascript
const element = React.createElement('h1', null, 'Hello, World!');
```

### 组件

组件是 React 应用的基本构建块，每个组件负责渲染 UI 的一部分。组件可以是函数组件或类组件。

#### 函数组件

函数组件是一个接收 props 并返回 React 元素的函数：

```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

#### 类组件

类组件是一个继承自 React.Component 的类，它通过 render 方法返回 React 元素：

```jsx
class Greeting extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}
```

### Props

Props（属性）是组件之间传递数据的方式，props 是只读的，组件不能修改自己的 props。

```jsx
// 父组件
function App() {
  return <Greeting name="John" />;
}

// 子组件
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

### State

State（状态）是组件内部的数据，用于存储组件的动态信息。当 state 发生变化时，React 会重新渲染组件。

#### 在类组件中使用 State

```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  increment = () => {
    this.setState(prevState => ({
      count: prevState.count + 1
    }));
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}
```

#### 在函数组件中使用 State（使用 Hooks）

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(prevCount => prevCount + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

### 生命周期

组件生命周期是指组件从创建到销毁的过程，React 提供了一系列生命周期方法，允许开发者在不同阶段执行代码。

#### 类组件生命周期方法

- **挂载阶段**：
  - `constructor`：组件初始化
  - `componentDidMount`：组件挂载到 DOM 后调用

- **更新阶段**：
  - `shouldComponentUpdate`：决定是否更新组件
  - `componentDidUpdate`：组件更新后调用

- **卸载阶段**：
  - `componentWillUnmount`：组件卸载前调用

#### 函数组件生命周期（使用 Hooks）

函数组件使用 `useEffect` Hook 来处理生命周期事件：

```jsx
import React, { useEffect } from 'react';

function Example() {
  // componentDidMount 和 componentDidUpdate
  useEffect(() => {
    console.log('Component mounted or updated');
    
    // componentWillUnmount
    return () => {
      console.log('Component will unmount');
    };
  }, [/* 依赖数组 */]);
  
  return <div>Example Component</div>;
}
```

### 事件处理

React 事件处理与 DOM 事件处理类似，但有一些语法差异：

- React 事件使用驼峰命名，而不是小写
- 事件处理函数是一个函数引用，而不是字符串
- 在类组件中，需要绑定 `this` 或使用箭头函数

```jsx
// 函数组件
function Button() {
  const handleClick = () => {
    console.log('Button clicked');
  };

  return <button onClick={handleClick}>Click me</button>;
}

// 类组件
class Button extends React.Component {
  handleClick = () => {
    console.log('Button clicked');
  };

  render() {
    return <button onClick={this.handleClick}>Click me</button>;
  }
}
```

## React Hooks

Hooks 是 React 16.8 引入的新特性，允许在函数组件中使用状态和其他 React 特性，而不需要编写类组件。

### useState

`useState` Hook 用于在函数组件中添加状态：

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('John');

  return (
    <div>
      <p>Count: {count}</p>
      <p>Name: {name}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setName('Jane')}>Change Name</button>
    </div>
  );
}
```

### useEffect

`useEffect` Hook 用于处理副作用，如数据获取、订阅或手动 DOM 操作：

```jsx
import React, { useState, useEffect } from 'react';

function DataFetching() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(data => setData(data));
  }, []); // 空依赖数组表示只在组件挂载时执行一次

  return (
    <div>
      {data.map(post => (
        <div key={post.id}>
          <h3>{post.title}</h3>
          <p>{post.body}</p>
        </div>
      ))}
    </div>
  );
}
```

### useContext

`useContext` Hook 用于访问 React Context，避免 props 层层传递：

```jsx
import React, { createContext, useContext } from 'react';

// 创建 Context
const ThemeContext = createContext('light');

// 父组件
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <ChildComponent />
    </ThemeContext.Provider>
  );
}

// 子组件
function ChildComponent() {
  // 使用 Context
  const theme = useContext(ThemeContext);
  return <div>Current theme: {theme}</div>;
}
```

### useReducer

`useReducer` Hook 用于复杂的状态管理，类似于 Redux：

```jsx
import React, { useReducer } from 'react';

// 定义 reducer
const counterReducer = (state, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
};

function Counter() {
  const [state, dispatch] = useReducer(counterReducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>Decrement</button>
    </div>
  );
}
```

### useCallback

`useCallback` Hook 用于缓存函数引用，避免不必要的重新渲染：

```jsx
import React, { useState, useCallback } from 'react';

function ParentComponent() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('John');

  // 只有当 count 变化时，才会重新创建 handleClick 函数
  const handleClick = useCallback(() => {
    console.log('Count:', count);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <p>Name: {name}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setName('Jane')}>Change Name</button>
      <ChildComponent onClick={handleClick} />
    </div>
  );
}

function ChildComponent({ onClick }) {
  return <button onClick={onClick}>Click me</button>;
}
```

### useMemo

`useMemo` Hook 用于缓存计算结果，避免不必要的重新计算：

```jsx
import React, { useState, useMemo } from 'react';

function ExpensiveCalculation() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('John');

  // 只有当 count 变化时，才会重新计算 expensiveValue
  const expensiveValue = useMemo(() => {
    console.log('Calculating expensive value...');
    return count * 2;
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <p>Name: {name}</p>
      <p>Expensive Value: {expensiveValue}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setName('Jane')}>Change Name</button>
    </div>
  );
}
```

### useRef

`useRef` Hook 用于创建一个可变的 ref 对象，其 `.current` 属性可以保存任意值：

```jsx
import React, { useRef, useEffect } from 'react';

function RefExample() {
  const inputRef = useRef(null);

  useEffect(() => {
    // 聚焦输入框
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} type="text" />;
}
```

### 自定义 Hooks

开发者可以创建自定义 Hooks，将组件逻辑提取到可复用的函数中：

```jsx
import React, { useState, useEffect } from 'react';

// 自定义 Hook：使用 localStorage 存储状态
function useLocalStorage(key, initialValue) {
  const [state, setState] = useState(() => {
    const storedValue = localStorage.getItem(key);
    return storedValue ? JSON.parse(storedValue) : initialValue;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(state));
  }, [key, state]);

  return [state, setState];
}

// 使用自定义 Hook
function Example() {
  const [name, setName] = useLocalStorage('name', 'John');

  return (
    <div>
      <p>Name: {name}</p>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
    </div>
  );
}
```

## React 生态

### React Router

React Router 是 React 应用的路由库，用于管理不同 URL 对应的组件：

```jsx
import React from 'react';
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function Home() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function App() {
  return (
    <BrowserRouter>
      <nav>
        <ul>
          <li><Link to="/">Home</Link></li>
          <li><Link to="/about">About</Link></li>
        </ul>
      </nav>
      
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

### 状态管理

- **Redux**：全局状态管理库，使用单一数据源和纯函数
- **MobX**：基于可观察对象的状态管理库
- **Zustand**：轻量级状态管理库，API 简单易用
- **Jotai**：基于原子的状态管理库

### 数据获取

- **React Query**：用于数据获取、缓存和同步的库
- **SWR**：用于远程数据获取的 React Hooks 库
- **Axios**：基于 Promise 的 HTTP 客户端

### UI 组件库

- **Material-UI**：基于 Material Design 的 React UI 组件库
- **Ant Design**：企业级 UI 设计语言和 React 组件库
- **Chakra UI**：简单、模块化、可访问的 React UI 组件库
- **Tailwind CSS**：实用优先的 CSS 框架

## React 最佳实践

1. **组件设计**：
   - 保持组件小而专注
   - 遵循单一职责原则
   - 使用函数组件和 Hooks

2. **状态管理**：
   - 尽量将状态下放到最需要的组件
   - 复杂状态使用状态管理库
   - 避免不必要的状态提升

3. **性能优化**：
   - 使用 `React.memo` 避免不必要的重新渲染
   - 使用 `useCallback` 和 `useMemo` 优化性能
   - 虚拟列表处理大量数据

4. **代码组织**：
   - 按功能或特性组织代码
   - 使用 TypeScript 提高代码质量
   - 编写清晰的组件文档

5. **测试**：
   - 使用 React Testing Library 进行测试
   - 编写单元测试和集成测试
   - 测试组件的渲染和交互

## 参考资源

- [React 官方文档](https://react.dev/)
- [React Router 官方文档](https://reactrouter.com/)
- [Redux 官方文档](https://redux.js.org/)
- [React Query 官方文档](https://tanstack.com/query/latest)
- [React Testing Library 官方文档](https://testing-library.com/docs/react-testing-library/intro/)
