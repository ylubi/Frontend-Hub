# Vue 核心概念

## 目录

- [什么是 Vue](#什么是-vue)
- [Vue 的特点](#vue-的特点)
- [Vue 版本对比](#vue-版本对比)
- [Vue 核心概念](#vue-核心概念)
  - [模板语法](#模板语法)
  - [组件](#组件)
  - [Props](#props)
  - [Data 与 Methods](#data-与-methods)
  - [生命周期](#生命周期)
  - [Computed 与 Watch](#computed-与-watch)
  - [指令](#指令)
  - [事件处理](#事件处理)
  - [组件通信](#组件通信)
- [Vue 3 Composition API](#vue-3-composition-api)
  - [setup 函数](#setup-函数)
  - [响应式系统](#响应式系统)
  - [组合式函数](#组合式函数)
  - [生命周期钩子](#生命周期钩子)
- [Vue 生态](#vue-生态)
  - [Vue Router](#vue-router)
  - [状态管理](#状态管理)
  - [UI 组件库](#ui-组件库)
  - [开发工具](#开发工具)
- [Vue 最佳实践](#vue-最佳实践)
- [参考资源](#参考资源)

## 什么是 Vue

Vue 是一套用于构建用户界面的渐进式 JavaScript 框架。与其他大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。

## Vue 的特点

1. **渐进式框架**：可以按需引入，逐步集成到现有项目中
2. **响应式数据绑定**：自动追踪数据变化并更新 DOM
3. **组件化开发**：支持组件复用和组合
4. **模板语法**：结合了 HTML 和 JavaScript 特性
5. **轻量级**：核心库体积小，加载速度快
6. **易于学习**：API 设计简洁明了
7. **强大的生态系统**：拥有丰富的官方和第三方库
8. **TypeScript 支持**：良好的 TypeScript 集成

## Vue 版本对比

| 特性 | Vue 2 | Vue 3 |
|------|-------|-------|
| 核心 API | Options API | Options API + Composition API |
| 响应式系统 | Object.defineProperty | Proxy |
| 性能 | 良好 | 更好（编译优化、虚拟 DOM 重写） |
| TypeScript 支持 | 一般 | 优秀 |
| 体积 | 较大 | 更小（Tree-shaking 支持） |
| 生命周期 | 与 Vue 3 类似，但有细微差别 | 新增 Composition API 生命周期 |
| 生态系统 | 成熟 | 正在发展中 |

## Vue 核心概念

### 模板语法

Vue 使用基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定到底层 Vue 实例的数据。

```html
<!-- 文本插值 -->
<h1>{{ message }}</h1>

<!-- 绑定属性 -->
<img v-bind:src="imageSrc" alt="图片">
<!-- 简写 -->
<img :src="imageSrc" alt="图片">

<!-- 条件渲染 -->
<div v-if="isVisible">可见内容</div>
<div v-else>不可见内容</div>

<!-- 列表渲染 -->
<ul>
  <li v-for="item in items" :key="item.id">{{ item.name }}</li>
</ul>

<!-- 事件处理 -->
<button v-on:click="handleClick">点击我</button>
<!-- 简写 -->
<button @click="handleClick">点击我</button>

<!-- 双向绑定 -->
<input v-model="inputValue" type="text">
```

### 组件

组件是 Vue 应用的基本构建块，每个组件都封装了自己的模板、逻辑和样式。

#### 单文件组件（SFC）

Vue 推荐使用单文件组件（.vue 文件），将模板、脚本和样式组织在同一个文件中：

```vue
<template>
  <div class="greeting">
    <h1>{{ message }}</h1>
    <button @click="changeMessage">改变消息</button>
  </div>
</template>

<script>
export default {
  name: 'Greeting',
  data() {
    return {
      message: 'Hello, Vue!'
    };
  },
  methods: {
    changeMessage() {
      this.message = 'Hello, World!';
    }
  }
};
</script>

<style scoped>
.greeting {
  color: blue;
}
</style>
```

#### 组件注册

- **全局注册**：
  ```javascript
  import Vue from 'vue';
  import Greeting from './components/Greeting.vue';
  
  Vue.component('Greeting', Greeting);
  ```

- **局部注册**：
  ```javascript
  import Greeting from './components/Greeting.vue';
  
  export default {
    components: {
      Greeting
    }
  };
  ```

### Props

Props 是组件之间传递数据的方式，父组件可以通过 props 向子组件传递数据。

```vue
<!-- 父组件 -->
<template>
  <ChildComponent :message="parentMessage" :count="10" />
</template>

<script>
export default {
  data() {
    return {
      parentMessage: 'Hello from parent'
    };
  }
};
</script>
```

```vue
<!-- 子组件 -->
<template>
  <div>
    <p>{{ message }}</p>
    <p>{{ count }}</p>
  </div>
</template>

<script>
export default {
  props: {
    // 基础类型检查
    message: String,
    // 带有默认值的数字
    count: {
      type: Number,
      default: 0
    },
    // 必需的字符串
    requiredProp: {
      type: String,
      required: true
    },
    // 自定义验证函数
    customProp: {
      validator: function(value) {
        return ['success', 'warning', 'error'].includes(value);
      }
    }
  }
};
</script>
```

### Data 与 Methods

- **Data**：组件的状态，是一个函数，返回一个对象
  ```javascript
export default {
  data() {
    return {
      count: 0,
      message: 'Hello'
    };
  }
};
  ```

- **Methods**：组件的方法，用于处理事件和业务逻辑
  ```javascript
export default {
  data() {
    return {
      count: 0
    };
  },
  methods: {
    increment() {
      this.count++;
    },
    decrement() {
      this.count--;
    }
  }
};
  ```

### 生命周期

Vue 组件从创建到销毁的过程中会触发一系列生命周期钩子函数。

#### Vue 2 生命周期

- **创建阶段**：
  - `beforeCreate`：实例初始化后，数据观测和事件配置之前调用
  - `created`：实例创建完成后调用，已完成数据观测、属性和方法的运算，事件回调的配置

- **挂载阶段**：
  - `beforeMount`：挂载开始之前调用
  - `mounted`：实例挂载到 DOM 后调用

- **更新阶段**：
  - `beforeUpdate`：数据更新之前调用
  - `updated`：组件 DOM 已经更新后调用

- **销毁阶段**：
  - `beforeDestroy`：实例销毁之前调用
  - `destroyed`：实例销毁后调用

#### Vue 3 生命周期

Vue 3 保留了大部分 Vue 2 的生命周期钩子，同时新增了 Composition API 生命周期钩子。

### Computed 与 Watch

- **Computed**：计算属性，基于响应式依赖进行缓存
  ```javascript
export default {
  data() {
    return {
      firstName: 'John',
      lastName: 'Doe'
    };
  },
  computed: {
    fullName() {
      return `${this.firstName} ${this.lastName}`;
    }
  }
};
  ```

- **Watch**：侦听器，用于观察和响应数据变化
  ```javascript
export default {
  data() {
    return {
      question: '',
      answer: '在您输入问题前我无法给您答案。'
    };
  },
  watch: {
    // 当 question 发生变化时，这个函数就会执行
    question(newQuestion, oldQuestion) {
      this.answer = '正在输入...';
      this.getAnswer();
    }
  },
  methods: {
    getAnswer() {
      // 模拟异步请求
      setTimeout(() => {
        this.answer = `这是您的问题: "${this.question}"`;
      }, 1000);
    }
  }
};
  ```

### 指令

Vue 提供了一些内置指令，用于简化 DOM 操作：

- `v-if` / `v-else` / `v-else-if`：条件渲染
- `v-for`：列表渲染
- `v-bind`：绑定属性
- `v-on`：绑定事件
- `v-model`：双向数据绑定
- `v-show`：条件显示（基于 CSS）
- `v-text`：更新元素的文本内容
- `v-html`：更新元素的 innerHTML
- `v-cloak`：防止页面闪烁
- `v-pre`：跳过编译过程
- `v-once`：只渲染一次

### 事件处理

Vue 事件处理与 DOM 事件处理类似，但有一些语法差异：

```html
<!-- 基本事件处理 -->
<button @click="handleClick">点击我</button>

<!-- 传递参数 -->
<button @click="handleClick('hello')">点击我</button>

<!-- 访问事件对象 -->
<button @click="handleClick($event, 'hello')">点击我</button>

<!-- 事件修饰符 -->
<button @click.stop="handleClick">阻止冒泡</button>
<button @click.prevent="handleClick">阻止默认行为</button>
<button @click.capture="handleClick">使用捕获模式</button>
<button @click.self="handleClick">只当事件在元素本身触发时执行</button>
<button @click.once="handleClick">只执行一次</button>

<!-- 按键修饰符 -->
<input @keyup.enter="handleEnter">
<input @keyup.esc="handleEsc">

<!-- 系统修饰符 -->
<input @click.ctrl="handleCtrlClick">
<input @click.alt="handleAltClick">
<input @click.shift="handleShiftClick">
<input @click.meta="handleMetaClick">
```

### 组件通信

Vue 组件间通信的主要方式：

1. **Props 向下传递**：父组件通过 props 向子组件传递数据
2. **事件向上传递**：子组件通过事件向父组件发送消息
3. **Event Bus**：通过事件总线在任意组件间通信
4. **Vuex/Pinia**：使用状态管理库管理全局状态
5. **Provide/Inject**：祖先组件向所有后代组件提供数据
6. **$parent/$children**：直接访问父/子组件实例
7. **$refs**：直接访问子组件 DOM 或实例

## Vue 3 Composition API

Vue 3 引入了 Composition API，它是一组基于函数的 API，允许开发者更灵活地组织组件逻辑。

### setup 函数

`setup` 函数是 Composition API 的入口点，在组件创建之前执行。

```vue
<template>
  <div>
    <p>Count: {{ count }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  setup() {
    // 响应式状态
    const count = ref(0);
    
    // 函数
    const increment = () => {
      count.value++;
    };
    
    // 生命周期钩子
    onMounted(() => {
      console.log('Component mounted');
    });
    
    // 返回值将暴露给模板和其他选项式 API 钩子
    return {
      count,
      increment
    };
  }
};
</script>
```

### 响应式系统

Vue 3 提供了以下响应式 API：

- **ref**：创建一个响应式的引用
  ```javascript
import { ref } from 'vue';

const count = ref(0);
console.log(count.value); // 0
count.value++;
  ```

- **reactive**：创建一个响应式对象
  ```javascript
import { reactive } from 'vue';

const state = reactive({
  count: 0,
  message: 'Hello'
});

state.count++;
  ```

- **computed**：创建一个计算属性
  ```javascript
import { ref, computed } from 'vue';

const count = ref(0);
const doubled = computed(() => count.value * 2);
  ```

- **watch**：创建一个侦听器
  ```javascript
import { ref, watch } from 'vue';

const count = ref(0);

watch(count, (newValue, oldValue) => {
  console.log(`Count changed from ${oldValue} to ${newValue}`);
});
  ```

### 组合式函数

组合式函数是封装和复用逻辑的函数，以 `use` 开头：

```javascript
// useCounter.js
import { ref, computed } from 'vue';

export function useCounter(initialValue = 0) {
  const count = ref(initialValue);
  
  const increment = () => {
    count.value++;
  };
  
  const decrement = () => {
    count.value--;
  };
  
  const reset = () => {
    count.value = initialValue;
  };
  
  const doubled = computed(() => count.value * 2);
  
  return {
    count,
    increment,
    decrement,
    reset,
    doubled
  };
}
```

```vue
<template>
  <div>
    <p>Count: {{ count }}</p>
    <p>Doubled: {{ doubled }}</p>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
    <button @click="reset">Reset</button>
  </div>
</template>

<script>
import { useCounter } from './useCounter';

export default {
  setup() {
    const { count, increment, decrement, reset, doubled } = useCounter(10);
    
    return {
      count,
      increment,
      decrement,
      reset,
      doubled
    };
  }
};
</script>
```

### 生命周期钩子

Composition API 提供了以下生命周期钩子：

- `onBeforeMount`：组件挂载前调用
- `onMounted`：组件挂载后调用
- `onBeforeUpdate`：组件更新前调用
- `onUpdated`：组件更新后调用
- `onBeforeUnmount`：组件卸载前调用
- `onUnmounted`：组件卸载后调用
- `onErrorCaptured`：捕获子组件错误
- `onRenderTracked`：跟踪渲染依赖
- `onRenderTriggered`：触发渲染时调用

## Vue 生态

### Vue Router

Vue Router 是 Vue 官方的路由管理器，用于构建单页应用。

```javascript
// router/index.js
import { createRouter, createWebHistory } from 'vue-router';
import Home from '../views/Home.vue';
import About from '../views/About.vue';

const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: About
  }
];

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
});

export default router;
```

### 状态管理

- **Vuex**：Vue 2 官方状态管理库
- **Pinia**：Vue 3 官方推荐的状态管理库，提供更简洁的 API

### UI 组件库

- **Element Plus**：基于 Vue 3 的企业级 UI 组件库
- **Ant Design Vue**：Ant Design 的 Vue 实现
- **Vuetify**：基于 Material Design 的 Vue UI 组件库
- **Naive UI**：一个 Vue 3 组件库

### 开发工具

- **Vue Devtools**：浏览器扩展，用于调试 Vue 应用
- **Vite**：下一代前端构建工具，提供极速的开发体验
- **Vue CLI**：Vue 2 官方脚手架工具

## Vue 最佳实践

1. **组件设计**：
   - 保持组件小而专注
   - 遵循单一职责原则
   - 使用语义化的组件名称

2. **状态管理**：
   - 尽量将状态下放到最需要的组件
   - 复杂状态使用 Vuex/Pinia
   - 避免直接修改 props

3. **性能优化**：
   - 使用 `v-for` 时添加 `key` 属性
   - 使用 `v-show` 替代 `v-if` 处理频繁切换的元素
   - 使用 `computed` 缓存计算结果
   - 使用 `keep-alive` 缓存组件状态

4. **代码组织**：
   - 使用单文件组件
   - 按功能组织代码
   - 使用 TypeScript 提高代码质量
   - 编写清晰的组件文档

5. **测试**：
   - 使用 Vue Test Utils 进行测试
   - 编写单元测试和集成测试
   - 测试组件的渲染和交互

## 参考资源

- [Vue 官方文档](https://vuejs.org/)
- [Vue Router 官方文档](https://router.vuejs.org/)
- [Pinia 官方文档](https://pinia.vuejs.org/)
- [Vue Test Utils 官方文档](https://test-utils.vuejs.org/)
- [Vite 官方文档](https://vite.dev/)
