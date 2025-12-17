# Svelte 核心概念

## 目录

- [什么是 Svelte](#什么是-svelte)
- [Svelte 的特点](#svelte-的特点)
- [Svelte 与其他框架的比较](#svelte-与其他框架的比较)
- [Svelte 核心概念](#svelte-核心概念)
  - [组件](#组件)
  - [响应式系统](#响应式系统)
  - [状态管理](#状态管理)
  - [事件处理](#事件处理)
  - [生命周期](#生命周期)
  - [组件通信](#组件通信)
  - [动画](#动画)
  - [条件渲染](#条件渲染)
  - [列表渲染](#列表渲染)
- [Svelte 生态](#svelte-生态)
  - [SvelteKit](#sveltekit)
  - [UI 组件库](#ui-组件库)
  - [状态管理库](#状态管理库)
  - [开发工具](#开发工具)
- [Svelte 最佳实践](#svelte-最佳实践)
- [参考资源](#参考资源)

## 什么是 Svelte

Svelte 是一个用于构建用户界面的现代 JavaScript 框架，由 Rich Harris 开发并开源。与 React 和 Vue 不同，Svelte 在构建时将组件编译为高效的 JavaScript 代码，而不是在运行时使用虚拟 DOM。

Svelte 的核心思想是 "编写更少的代码，获得更好的性能"。它通过在构建时分析组件，生成高效的 DOM 操作代码，从而避免了运行时的性能开销。

## Svelte 的特点

1. **无虚拟 DOM**：在构建时编译为原生 DOM 操作，性能更高
2. **响应式系统**：自动追踪变量的依赖关系，无需手动管理
3. **简洁的语法**：使用类似 HTML 的模板语法，学习曲线平缓
4. **轻量级**：生成的代码体积小，加载速度快
5. **组件化**：支持组件复用和组合
6. **内置动画**：提供强大的动画支持，无需第三方库
7. **TypeScript 支持**：良好的 TypeScript 集成
8. **易于学习**：API 设计简洁明了
9. **良好的性能**：运行时性能优异
10. **丰富的生态系统**：拥有 SvelteKit 等工具

## Svelte 与其他框架的比较

| 特性 | Svelte | React | Vue |
|------|--------|-------|-----|
| 类型 | 框架 | 库 | 渐进式框架 |
| 渲染方式 | 编译时 | 运行时 + 编译时 | 运行时 + 编译时 |
| 虚拟 DOM | 无 | 有 | 有 |
| 响应式系统 | 编译时追踪 | useState/useEffect | 响应式数据绑定 |
| 语法 | .svelte 文件 | JSX | 模板语法 |
| 性能 | 优秀 | 良好 | 良好 |
| 学习曲线 | 平缓 | 中等 | 平缓 |
| 生态系统 | 正在发展中 | 成熟 | 成熟 |
| 适合项目 | 各种规模 | 各种规模 | 各种规模 |
| 构建工具 | SvelteKit/Vite | Webpack/Vite | Vue CLI/Vite |

## Svelte 核心概念

### 组件

Svelte 组件是一个包含模板、脚本和样式的 .svelte 文件。

#### 组件结构

```svelte
<!-- App.svelte -->
<script>
  let name = 'World';
  
  function greet() {
    console.log(`Hello, ${name}!`);
  }
</script>

<h1>Hello, {name}!</h1>
<button on:click={greet}>点击我</button>

<style>
h1 {
  color: blue;
}

button {
  background-color: lightgray;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
```

#### 组件导入和使用

```svelte
<!-- ParentComponent.svelte -->
<script>
  import ChildComponent from './ChildComponent.svelte';
  
  let message = 'Hello from parent';
</script>

<ChildComponent message={message} />
```

```svelte
<!-- ChildComponent.svelte -->
<script>
  export let message;
</script>

<p>{message}</p>
```

### 响应式系统

Svelte 的响应式系统是其核心特性之一，它允许开发者声明式地定义变量，Svelte 会自动追踪变量的依赖关系并更新 DOM。

#### 基本响应式

```svelte
<script>
  let count = 0;
  
  function increment() {
    count += 1;
  }
</script>

<p>Count: {count}</p>
<button on:click={increment}>Increment</button>
```

#### 响应式数组和对象

```svelte
<script>
  let numbers = [1, 2, 3];
  let person = { name: 'John', age: 30 };
  
  function addNumber() {
    numbers = [...numbers, numbers.length + 1];
  }
  
  function updatePerson() {
    person = { ...person, age: person.age + 1 };
  }
</script>

<ul>
  {#each numbers as number}
    <li>{number}</li>
  {/each}
</ul>
<button on:click={addNumber}>Add Number</button>

<p>Name: {person.name}, Age: {person.age}</p>
<button on:click={updatePerson}>Update Age</button>
```

#### 响应式声明

使用 `$:` 语法创建响应式声明，当依赖变量变化时自动重新计算：

```svelte
<script>
  let a = 1;
  let b = 2;
  
  // 响应式声明，当 a 或 b 变化时自动更新
  $: sum = a + b;
  $: {
    console.log(`Sum is now ${sum}`);
  }
</script>

<p>a: <input type="number" bind:value={a}></p>
<p>b: <input type="number" bind:value={b}></p>
<p>Sum: {sum}</p>
```

### 状态管理

Svelte 提供了多种状态管理方式，包括组件状态、上下文 API 和第三方库。

#### 组件状态

```svelte
<script>
  let count = 0;
</script>

<p>Count: {count}</p>
<button on:click={() => count++}>Increment</button>
```

#### 上下文 API

使用 `setContext` 和 `getContext` 在组件树中共享状态：

```svelte
<!-- App.svelte -->
<script>
  import { setContext } from 'svelte';
  import ChildComponent from './ChildComponent.svelte';
  
  const countContext = { count: 0 };
  setContext('count', countContext);
  
  function increment() {
    countContext.count += 1;
  }
</script>

<p>Count: {countContext.count}</p>
<button on:click={increment}>Increment</button>
<ChildComponent />
```

```svelte
<!-- ChildComponent.svelte -->
<script>
  import { getContext } from 'svelte';
  
  const countContext = getContext('count');
</script>

<p>Child Count: {countContext.count}</p>
```

#### 可写存储

使用 `writable` 创建可写的响应式存储：

```javascript
// store.js
import { writable } from 'svelte/store';

export const count = writable(0);
```

```svelte
<!-- Component.svelte -->
<script>
  import { count } from './store.js';
  
  function increment() {
    count.update(n => n + 1);
  }
  
  function reset() {
    count.set(0);
  }
</script>

<!-- 使用 $ 前缀访问存储值 -->
<p>Count: {$count}</p>
<button on:click={increment}>Increment</button>
<button on:click={reset}>Reset</button>
```

#### 只读存储

使用 `readable` 创建只读的响应式存储：

```javascript
// store.js
import { readable } from 'svelte/store';

export const time = readable(new Date(), function start(set) {
  const interval = setInterval(() => {
    set(new Date());
  }, 1000);
  
  return function stop() {
    clearInterval(interval);
  };
});
```

```svelte
<!-- Component.svelte -->
<script>
  import { time } from './store.js';
</script>

<p>Current time: {$time.toLocaleTimeString()}</p>
```

#### 派生存储

使用 `derived` 从现有存储创建派生存储：

```javascript
// store.js
import { writable, derived } from 'svelte/store';

export const count = writable(0);
export const doubled = derived(count, $count => $count * 2);
export const tripled = derived(count, $count => $count * 3);
```

```svelte
<!-- Component.svelte -->
<script>
  import { count, doubled, tripled } from './store.js';
</script>

<p>Count: {$count}</p>
<p>Doubled: {$doubled}</p>
<p>Tripled: {$tripled}</p>
<button on:click={() => count.update(n => n + 1)}>Increment</button>
```

### 事件处理

Svelte 使用 `on:` 指令处理事件。

#### 基本事件处理

```svelte
<script>
  function handleClick() {
    console.log('Button clicked');
  }
  
  function handleInput(event) {
    console.log('Input value:', event.target.value);
  }
</script>

<button on:click={handleClick}>Click me</button>
<input on:input={handleInput} placeholder="Type something">
```

#### 事件修饰符

Svelte 提供了多种事件修饰符：

```svelte
<!-- 阻止默认行为 -->
<a href="#" on:click|preventDefault={handleClick}>Click me</a>

<!-- 阻止冒泡 -->
<div on:click={handleParentClick}>
  <button on:click|stopPropagation={handleChildClick}>Click me</button>
</div>

<!-- 只触发一次 -->
<button on:click|once={handleClick}>Click me once</button>

<!-- 键盘事件修饰符 -->
<input on:keydown|enter={handleEnter} placeholder="Press Enter">
<input on:keydown|escape={handleEscape} placeholder="Press Escape">

<!-- 鼠标事件修饰符 -->
<div on:mousedown|left={handleLeftClick}>Left click</div>
<div on:mousedown|right={handleRightClick}>Right click</div>
```

#### 组件事件

组件可以通过 `createEventDispatcher` 分发事件：

```svelte
<!-- ChildComponent.svelte -->
<script>
  import { createEventDispatcher } from 'svelte';
  
  const dispatch = createEventDispatcher();
  
  function handleClick() {
    dispatch('customclick', { message: 'Hello from child' });
  }
</script>

<button on:click={handleClick}>Click me</button>
```

```svelte
<!-- ParentComponent.svelte -->
<script>
  import ChildComponent from './ChildComponent.svelte';
  
  function handleCustomClick(event) {
    console.log('Custom event received:', event.detail.message);
  }
</script>

<ChildComponent on:customclick={handleCustomClick} />
```

### 生命周期

Svelte 提供了四个生命周期钩子：

1. **onMount**：组件挂载到 DOM 后调用
2. **onDestroy**：组件卸载前调用
3. **beforeUpdate**：组件更新前调用
4. **afterUpdate**：组件更新后调用

```svelte
<script>
  import { onMount, onDestroy, beforeUpdate, afterUpdate } from 'svelte';
  
  let count = 0;
  
  onMount(() => {
    console.log('Component mounted');
    
    // 清理函数
    return () => {
      console.log('Component will unmount');
    };
  });
  
  onDestroy(() => {
    console.log('Component destroyed');
  });
  
  beforeUpdate(() => {
    console.log('Before update');
  });
  
  afterUpdate(() => {
    console.log('After update');
  });
  
  function increment() {
    count += 1;
  }
</script>

<p>Count: {count}</p>
<button on:click={increment}>Increment</button>
```

### 组件通信

Svelte 组件间通信可以通过以下方式实现：

1. **Props**：父组件向子组件传递数据
2. **组件事件**：子组件向父组件发送消息
3. **上下文 API**：组件树中共享数据
4. **存储**：全局状态管理

#### Props

```svelte
<!-- ParentComponent.svelte -->
<script>
  import ChildComponent from './ChildComponent.svelte';
  
  let message = 'Hello from parent';
</script>

<ChildComponent message={message} />
```

```svelte
<!-- ChildComponent.svelte -->
<script>
  export let message;
</script>

<p>{message}</p>
```

#### 组件事件

```svelte
<!-- ParentComponent.svelte -->
<script>
  import ChildComponent from './ChildComponent.svelte';
  
  function handleCustomEvent(event) {
    console.log('Custom event:', event.detail);
  }
</script>

<ChildComponent on:custom-event={handleCustomEvent} />
```

```svelte
<!-- ChildComponent.svelte -->
<script>
  import { createEventDispatcher } from 'svelte';
  
  const dispatch = createEventDispatcher();
  
  function sendEvent() {
    dispatch('custom-event', { data: 'Hello' });
  }
</script>

<button on:click={sendEvent}>Send Event</button>
```

### 动画

Svelte 内置了强大的动画支持，无需第三方库。

#### 基本动画

```svelte
<script>
  import { fade } from 'svelte/transition';
  
  let visible = true;
</script>

<button on:click={() => visible = !visible}>Toggle</button>

{#if visible}
  <div transition:fade>
    <p>Hello, World!</p>
  </div>
{/if}
```

#### 带参数的动画

```svelte
<script>
  import { fade, slide, scale } from 'svelte/transition';
  
  let visible = true;
</script>

<button on:click={() => visible = !visible}>Toggle</button>

{#if visible}
  <div transition:fade={{ duration: 500 }}>
    <p>Fade</p>
  </div>
  
  <div transition:slide={{ delay: 200, duration: 300 }}>
    <p>Slide</p>
  </div>
  
  <div transition:scale={{ start: 0.5, duration: 400 }}>
    <p>Scale</p>
  </div>
{/if}
```

#### 自定义动画

```svelte
<script>
  import { cubicOut } from 'svelte/easing';
  
  let visible = true;
  
  function customTransition(node, { delay = 0, duration = 400 }) {
    const style = getComputedStyle(node);
    const opacity = +style.opacity;
    const transform = style.transform === 'none' ? '' : style.transform;
    
    return {
      delay,
      duration,
      easing: cubicOut,
      css: t => {
        return `
          opacity: ${t * opacity};
          transform: ${transform} scale(${t});
        `;
      }
    };
  }
</script>

<button on:click={() => visible = !visible}>Toggle</button>

{#if visible}
  <div transition:customTransition>
    <p>Custom Animation</p>
  </div>
{/if}
```

### 条件渲染

Svelte 使用 `{#if}` 指令进行条件渲染。

```svelte
<script>
  let count = 0;
</script>

{#if count > 10}
  <p>Count is greater than 10</p>
{:else if count > 5}
  <p>Count is greater than 5 but less than or equal to 10</p>
{:else}
  <p>Count is less than or equal to 5</p>
{/if}

<button on:click={() => count += 1}>Increment</button>
<p>Count: {count}</p>
```

### 列表渲染

Svelte 使用 `{#each}` 指令进行列表渲染。

```svelte
<script>
  let items = [
    { id: 1, name: 'Item 1' },
    { id: 2, name: 'Item 2' },
    { id: 3, name: 'Item 3' }
  ];
  
  function addItem() {
    items = [...items, { id: items.length + 1, name: `Item ${items.length + 1}` }];
  }
  
  function removeItem(id) {
    items = items.filter(item => item.id !== id);
  }
</script>

<ul>
  {#each items as item, index}
    <li>
      {index + 1}: {item.name}
      <button on:click={() => removeItem(item.id)}>Remove</button>
    </li>
  {/each}
</ul>

<button on:click={addItem}>Add Item</button>
```

## Svelte 生态

### SvelteKit

SvelteKit 是 Svelte 的官方应用框架，用于构建生产级别的 Svelte 应用。它提供了路由、服务端渲染、静态站点生成等功能。

#### SvelteKit 特点

1. **文件系统路由**：基于文件结构自动生成路由
2. **服务端渲染**：支持 SSR 和 SSG
3. **API 路由**：轻松创建 API 端点
4. **自动代码分割**：优化加载性能
5. **TypeScript 支持**：内置 TypeScript 支持
6. **开发服务器**：快速的开发体验

#### SvelteKit 项目结构

```
sveltekit-project/
├── src/
│   ├── lib/          # 共享库和组件
│   ├── routes/       # 路由页面
│   │   ├── +layout.svelte    # 根布局
│   │   ├── +page.svelte      # 首页
│   │   └── about/           # 关于页
│   │       └── +page.svelte
│   └── app.html      # HTML 模板
├── static/           # 静态资源
└── package.json
```

### UI 组件库

1. **Svelte Material UI**：Material Design 风格的 UI 组件库
2. **Carbon Components Svelte**：IBM Carbon Design System 的 Svelte 实现
3. **SvelteStrap**：Bootstrap 的 Svelte 实现
4. **Flowbite Svelte**：Tailwind CSS 组件库
5. **Skeleton**：轻量级 UI 工具包

### 状态管理库

1. **Svelte Stores**：Svelte 内置的状态管理
2. **Zustand**：轻量级状态管理库，支持 Svelte
3. **Jotai**：原子化状态管理库
4. **XState**：状态机库

### 开发工具

1. **Svelte DevTools**：浏览器扩展，用于调试 Svelte 应用
2. **Vite**：下一代前端构建工具，支持 Svelte
3. **Svelte Language Server**：VS Code 扩展，提供代码补全和语法高亮
4. **Svelte Check**：静态类型检查工具

## Svelte 最佳实践

1. **组件设计**：
   - 保持组件小而专注
   - 遵循单一职责原则
   - 使用语义化的组件名称
   - 合理划分组件边界

2. **响应式设计**：
   - 优先使用 Svelte 的响应式系统
   - 避免过度使用存储
   - 合理使用响应式声明

3. **性能优化**：
   - 使用 `key` 优化列表渲染
   - 避免不必要的重新渲染
   - 合理使用动画
   - 实现虚拟滚动处理大量数据

4. **代码组织**：
   - 按功能组织代码
   - 使用 TypeScript 提高代码质量
   - 编写清晰的组件文档
   - 合理使用注释

5. **测试**：
   - 使用 Vitest 进行单元测试
   - 使用 Playwright 进行 E2E 测试
   - 测试组件的渲染和交互

6. **样式设计**：
   - 使用组件作用域样式
   - 避免全局样式冲突
   - 合理使用 CSS 预处理器
   - 考虑使用 CSS 框架

## 参考资源

- [Svelte 官方文档](https://svelte.dev/docs)
- [SvelteKit 官方文档](https://kit.svelte.dev/docs)
- [Svelte 教程](https://svelte.dev/tutorial)
- [Svelte 示例](https://svelte.dev/examples)
- [Svelte 博客](https://svelte.dev/blog)
- [Svelte 社区](https://svelte.dev/community)
- [Svelte 生态系统](https://svelte.dev/ecosystem)
