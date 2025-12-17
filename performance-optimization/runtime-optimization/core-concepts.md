# 运行时优化

运行时优化是指在网页运行过程中，通过各种技术手段提高网页的响应速度和运行效率，减少资源消耗。

## 1. 内存管理

### 1.1 内存管理的重要性

- 避免内存泄漏，防止页面卡顿或崩溃
- 提高页面的响应速度
- 减少浏览器资源消耗
- 延长移动设备的电池寿命

### 1.2 常见的内存泄漏场景

#### 1.2.1 意外的全局变量

```javascript
// 意外创建全局变量
function leak() {
  leakVar = "This is a leak";
  // 等价于 window.leakVar = "This is a leak";
}

// 解决方案：使用严格模式
'use strict';
function noLeak() {
  const noLeakVar = "This is not a leak";
}
```

#### 1.2.2 闭包导致的内存泄漏

```javascript
// 闭包导致的内存泄漏
function createLeak() {
  const element = document.getElementById('element');
  const handler = () => {
    console.log(element.id);
  };
  element.addEventListener('click', handler);
  // 没有移除事件监听器，element 和 handler 都不会被垃圾回收
}

// 解决方案：移除事件监听器
function noLeak() {
  const element = document.getElementById('element');
  const handler = () => {
    console.log(element.id);
  };
  element.addEventListener('click', handler);
  // 在适当的时候移除事件监听器
  element.removeEventListener('click', handler);
}
```

#### 1.2.3 未清理的定时器

```javascript
// 未清理的定时器
function createLeak() {
  const data = {};
  setInterval(() => {
    console.log(data);
  }, 1000);
  // 定时器没有被清除，data 不会被垃圾回收
}

// 解决方案：清理定时器
function noLeak() {
  const data = {};
  const timerId = setInterval(() => {
    console.log(data);
  }, 1000);
  // 在适当的时候清除定时器
  clearInterval(timerId);
}
```

#### 1.2.4 DOM 引用

```javascript
// DOM 引用导致的内存泄漏
function createLeak() {
  const elements = [];
  const element = document.getElementById('element');
  elements.push(element);
  document.body.removeChild(element);
  // element 仍然被 elements 数组引用，不会被垃圾回收
}

// 解决方案：移除 DOM 引用
function noLeak() {
  const elements = [];
  const element = document.getElementById('element');
  elements.push(element);
  document.body.removeChild(element);
  // 移除 DOM 引用
  elements.pop();
}
```

### 1.3 内存管理最佳实践

- 使用严格模式，避免意外创建全局变量
- 及时移除事件监听器
- 清理定时器和间隔器
- 避免闭包中引用不必要的大对象
- 减少 DOM 引用，及时移除不再使用的 DOM 元素
- 使用 WeakMap 和 WeakSet 存储对象引用，允许垃圾回收
- 定期检查内存使用情况，使用 Chrome DevTools Memory 面板进行分析

## 2. 事件委托

### 2.1 事件委托的原理

事件委托是利用事件冒泡机制，将事件监听器添加到父元素上，而不是每个子元素上，从而减少事件监听器的数量。

### 2.2 事件委托的优势

- 减少事件监听器的数量，降低内存消耗
- 动态添加的子元素无需重新绑定事件
- 提高性能，特别是在有大量子元素的情况下

### 2.3 事件委托的实现

```javascript
// 传统方式：为每个子元素添加事件监听器
const items = document.querySelectorAll('.item');
items.forEach(item => {
  item.addEventListener('click', () => {
    console.log(item.textContent);
  });
});

// 事件委托：为父元素添加事件监听器
const container = document.querySelector('.container');
container.addEventListener('click', (e) => {
  if (e.target.classList.contains('item')) {
    console.log(e.target.textContent);
  }
});
```

### 2.4 事件委托的最佳实践

- 选择合适的父元素，避免层级过深
- 使用 event.target 准确判断事件源
- 注意事件冒泡和捕获阶段的区别
- 对于需要阻止冒泡的事件，使用 event.stopPropagation()

## 3. Web Workers

### 3.1 Web Workers 的原理

Web Workers 允许在后台线程中运行 JavaScript 代码，与主线程并行执行，不会阻塞主线程。

### 3.2 Web Workers 的类型

- **Dedicated Workers**：专用 Worker，只能被创建它的脚本使用
- **Shared Workers**：共享 Worker，可以被多个脚本使用
- **Service Workers**：用于离线缓存和推送通知

### 3.3 Web Workers 的使用场景

- 复杂的计算任务
- 数据处理和分析
- 图像处理
- 后台网络请求
- 实时数据处理

### 3.4 Web Workers 的实现

```javascript
// 主线程代码
const worker = new Worker('worker.js');

// 向 Worker 发送数据
worker.postMessage({ type: 'calculate', data: [1, 2, 3, 4, 5] });

// 接收 Worker 返回的数据
worker.onmessage = (e) => {
  console.log('Result:', e.data.result);
};

// 处理错误
worker.onerror = (e) => {
  console.error('Worker error:', e.message);
};

// worker.js
self.onmessage = (e) => {
  if (e.data.type === 'calculate') {
    const result = e.data.data.reduce((sum, num) => sum + num, 0);
    // 向主线程发送结果
    self.postMessage({ result });
  }
};
```

### 3.5 Web Workers 的限制

- 不能直接访问 DOM
- 不能使用 window 对象
- 不能使用 document 对象
- 不能使用 parent 对象
- 受同源策略限制

### 3.6 Web Workers 的最佳实践

- 只在需要时创建 Worker，用完后关闭
- 合理设计 Worker 和主线程之间的通信
- 避免频繁发送大量数据
- 考虑浏览器兼容性

## 4. 防抖与节流

### 4.1 防抖（Debounce）

防抖是指在事件触发后，等待一段时间再执行回调函数，如果在这段时间内事件再次触发，则重新开始计时。

### 4.2 防抖的使用场景

- 搜索输入框实时搜索
- 窗口大小调整
- 滚动事件
- 表单验证

### 4.3 防抖的实现

```javascript
function debounce(func, delay) {
  let timerId;
  return function(...args) {
    clearTimeout(timerId);
    timerId = setTimeout(() => {
      func.apply(this, args);
    }, delay);
  };
}

// 使用防抖
const searchInput = document.querySelector('.search-input');
searchInput.addEventListener('input', debounce((e) => {
  console.log('Searching:', e.target.value);
}, 300));
```

### 4.4 节流（Throttle）

节流是指在一段时间内，只执行一次回调函数，无论事件触发多少次。

### 4.5 节流的使用场景

- 滚动事件
- 鼠标移动事件
- 游戏中的射击或移动操作
- 频繁点击按钮

### 4.6 节流的实现

```javascript
function throttle(func, delay) {
  let lastCall = 0;
  return function(...args) {
    const now = Date.now();
    if (now - lastCall >= delay) {
      lastCall = now;
      func.apply(this, args);
    }
  };
}

// 使用节流
window.addEventListener('scroll', throttle(() => {
  console.log('Scrolling:', window.scrollY);
}, 200));
```

### 4.7 防抖与节流的区别

- **防抖**：事件触发后等待一段时间再执行，适用于需要等待用户停止操作的场景
- **节流**：一段时间内只执行一次，适用于需要限制执行频率的场景

## 5. 其他运行时优化技术

### 5.1 减少重排重绘

- **重排（Reflow）**：元素的几何属性发生变化，导致浏览器重新计算布局
- **重绘（Repaint）**：元素的外观发生变化，但几何属性不变

**优化建议**：
- 使用 `transform` 和 `opacity` 代替 `top`、`left` 等属性进行动画
- 避免频繁操作 DOM
- 使用文档片段（DocumentFragment）批量更新 DOM
- 避免使用 table 布局
- 使用 CSS 硬件加速

### 5.2 优化 JavaScript 执行

- 减少主线程阻塞，将耗时操作移至 Web Workers
- 优化循环和算法，减少计算复杂度
- 使用 requestAnimationFrame 进行动画
- 避免使用 eval 和 with
- 优化闭包，避免不必要的变量捕获

### 5.3 优化网络请求

- 使用 HTTP/2 或 HTTP/3
- 减少请求数量，合并请求
- 使用 CDN 加速
- 实现有效的缓存策略
- 使用 WebSockets 或 Server-Sent Events 进行实时通信

### 5.4 优化数据结构和算法

- 选择合适的数据结构，如 Map、Set 等
- 优化算法复杂度，避免 O(n²) 或更高复杂度的算法
- 使用二分查找、哈希表等高效算法
- 减少不必要的数据转换和复制

## 6. 运行时优化最佳实践

1. **监控内存使用**：使用 Chrome DevTools Memory 面板定期检查内存使用情况
2. **减少事件监听器**：使用事件委托，及时移除不再需要的事件监听器
3. **合理使用 Web Workers**：将耗时操作移至后台线程
4. **使用防抖和节流**：限制函数的执行频率
5. **优化 DOM 操作**：减少重排重绘，批量更新 DOM
6. **优化 JavaScript 执行**：减少主线程阻塞，优化算法
7. **监控性能指标**：使用 Performance API 监控关键性能指标
8. **持续优化**：定期分析和优化代码，保持良好的性能

## 7. 工具和资源

- **Chrome DevTools**：内存分析、性能分析
- **Lighthouse**：网站性能评估
- **WebPageTest**：网站性能测试
- **Performance API**：JavaScript 性能监控
- **Memory API**：JavaScript 内存监控

运行时优化是前端性能优化的重要组成部分，通过合理的内存管理、事件处理、线程管理和算法优化，可以显著提高网页的运行效率和响应速度，提升用户体验。