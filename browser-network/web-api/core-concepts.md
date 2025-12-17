# Web API

Web API 是浏览器提供的一系列 JavaScript API，用于访问浏览器功能和网页内容。Web API 是前端开发的重要组成部分，允许开发者创建丰富的交互式网页应用。

## 1. Web API 的分类

### 1.1 DOM API

DOM (Document Object Model) API 用于访问和操作 HTML 文档的结构和内容。

#### 1.1.1 核心 DOM API

- **Document**：表示整个 HTML 文档
- **Element**：表示 HTML 元素
- **Node**：表示文档中的节点（元素、文本、注释等）
- **Attribute**：表示 HTML 元素的属性
- **Event**：表示事件

#### 1.1.2 常用 DOM 操作

```javascript
// 选择元素
const element = document.getElementById('id');
const elements = document.querySelectorAll('.class');
const elementsByTag = document.getElementsByTagName('tag');
const elementsByName = document.getElementsByName('name');

// 创建和添加元素
const newElement = document.createElement('div');
newElement.textContent = 'Hello, World!';
document.body.appendChild(newElement);

// 修改元素
const element = document.querySelector('.element');
element.innerHTML = '<p>New content</p>';
element.style.color = 'red';
element.setAttribute('data-id', '123');

// 删除元素
const element = document.querySelector('.element');
element.remove();

// 事件处理
element.addEventListener('click', (e) => {
  console.log('Element clicked');
});

element.removeEventListener('click', handler);
```

### 1.2 BOM API

BOM (Browser Object Model) API 用于访问和操作浏览器窗口和导航。

#### 1.2.1 核心 BOM API

- **Window**：表示浏览器窗口
- **Navigator**：表示浏览器信息
- **Location**：表示当前 URL
- **History**：表示浏览器历史记录
- **Screen**：表示屏幕信息

#### 1.2.2 常用 BOM 操作

```javascript
// Window 对象
window.alert('Hello, World!');
window.confirm('Are you sure?');
window.prompt('What is your name?');
window.setTimeout(() => {
  console.log('Timeout');
}, 1000);
window.setInterval(() => {
  console.log('Interval');
}, 1000);

// Navigator 对象
console.log(navigator.userAgent);
console.log(navigator.language);
console.log(navigator.onLine);

// Location 对象
console.log(location.href);
console.log(location.pathname);
location.reload();
location.assign('https://example.com');

// History 对象
history.back();
history.forward();
history.go(-1);

// Screen 对象
console.log(screen.width);
console.log(screen.height);
console.log(screen.availWidth);
console.log(screen.availHeight);
```

### 1.3 Fetch API

Fetch API 用于进行网络请求，替代传统的 XMLHttpRequest。

#### 1.3.1 基本用法

```javascript
// GET 请求
fetch('https://api.example.com/data')
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('Error:', error);
  });

// POST 请求
fetch('https://api.example.com/data', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'Alice',
    age: 30
  })
})
  .then(response => response.json())
  .then(data => console.log(data));

// 配置选项
fetch('https://api.example.com/data', {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer token'
  },
  mode: 'cors',
  cache: 'no-cache',
  credentials: 'include'
});
```

#### 1.3.2 Fetch API 的优势

- 基于 Promise，使用更简洁
- 支持流式处理
- 更好的错误处理
- 支持 CORS 和其他现代网络特性

### 1.4 Web Storage API

Web Storage API 用于在浏览器中存储数据，包括 localStorage 和 sessionStorage。

#### 1.4.1 localStorage

localStorage 用于长期存储数据，数据不会过期，除非手动删除。

```javascript
// 存储数据
localStorage.setItem('name', 'Alice');
localStorage.setItem('age', '30');

// 获取数据
const name = localStorage.getItem('name');
const age = localStorage.getItem('age');

// 删除数据
localStorage.removeItem('name');

// 清空所有数据
localStorage.clear();
```

#### 1.4.2 sessionStorage

sessionStorage 用于临时存储数据，数据在会话结束时（关闭浏览器窗口或标签页）删除。

```javascript
// 存储数据
sessionStorage.setItem('name', 'Alice');
sessionStorage.setItem('age', '30');

// 获取数据
const name = sessionStorage.getItem('name');
const age = sessionStorage.getItem('age');

// 删除数据
sessionStorage.removeItem('name');

// 清空所有数据
sessionStorage.clear();
```

### 1.5 IndexedDB

IndexedDB 是一种用于浏览器的低级异步数据库 API，用于存储大量结构化数据。

#### 1.5.1 基本用法

```javascript
// 打开数据库
const request = indexedDB.open('myDatabase', 1);

request.onerror = (event) => {
  console.error('Database error:', event.target.error);
};

request.onupgradeneeded = (event) => {
  const db = event.target.result;
  
  // 创建对象存储
  const objectStore = db.createObjectStore('users', { keyPath: 'id' });
  
  // 创建索引
  objectStore.createIndex('name', 'name', { unique: false });
  objectStore.createIndex('email', 'email', { unique: true });
};

request.onsuccess = (event) => {
  const db = event.target.result;
  
  // 执行数据库操作
  addUser(db, { id: 1, name: 'Alice', email: 'alice@example.com' });
  getUser(db, 1);
};

// 添加数据
function addUser(db, user) {
  const transaction = db.transaction(['users'], 'readwrite');
  const store = transaction.objectStore('users');
  const request = store.add(user);
  
  request.onsuccess = () => {
    console.log('User added successfully');
  };
}

// 获取数据
function getUser(db, id) {
  const transaction = db.transaction(['users'], 'readonly');
  const store = transaction.objectStore('users');
  const request = store.get(id);
  
  request.onsuccess = () => {
    console.log('User:', request.result);
  };
}
```

### 1.6 其他常用 Web API

#### 1.6.1 Web Audio API

用于处理音频，包括播放、录制、合成等。

#### 1.6.2 Web Speech API

用于语音识别和语音合成。

```javascript
// 语音合成
const synth = window.speechSynthesis;
const utterance = new SpeechSynthesisUtterance('Hello, World!');
synth.speak(utterance);

// 语音识别
const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
recognition.onresult = (event) => {
  const speechResult = event.results[0][0].transcript;
  console.log('Speech result:', speechResult);
};
recognition.start();
```

#### 1.6.3 WebXR API

用于创建虚拟现实（VR）和增强现实（AR）体验。

#### 1.6.4 Web Workers

用于在后台线程中运行 JavaScript 代码，避免阻塞主线程。

#### 1.6.5 Service Workers

用于离线缓存、推送通知和后台同步。

#### 1.6.6 WebSockets

用于在浏览器和服务器之间建立双向通信。

```javascript
// 创建 WebSocket 连接
const socket = new WebSocket('ws://example.com');

// 连接打开
 socket.addEventListener('open', (event) => {
  socket.send('Hello, Server!');
});

// 接收消息
socket.addEventListener('message', (event) => {
  console.log('Message from server:', event.data);
});

// 连接关闭
socket.addEventListener('close', (event) => {
  console.log('Connection closed');
});

// 发生错误
socket.addEventListener('error', (event) => {
  console.error('WebSocket error:', event);
});
```

## 2. Web API 最佳实践

1. **检查 API 可用性**：在使用不常用或新的 API 之前，检查浏览器是否支持
   ```javascript
   if ('fetch' in window) {
     // 使用 fetch API
   } else {
     // 使用 XMLHttpRequest 作为备选
   }
   ```

2. **处理错误**：始终为 API 调用添加错误处理

3. **使用适当的 API**：根据需求选择合适的 API，例如：
   - 小量数据使用 Web Storage
   - 大量结构化数据使用 IndexedDB
   - 网络请求使用 Fetch API

4. **考虑性能**：
   - 避免在主线程上执行大量计算，使用 Web Workers
   - 优化 DOM 操作，减少重排重绘
   - 合理使用缓存

5. **保护用户隐私**：
   - 尊重用户的隐私设置
   - 不要滥用地理位置、摄像头等敏感 API
   - 遵循浏览器的权限政策

6. **保持代码简洁**：使用模块化和封装，提高代码的可维护性

## 3. Web API 学习资源

- [MDN Web API 文档](https://developer.mozilla.org/en-US/docs/Web/API)
- [Web APIs - Can I use](https://caniuse.com/)
- [Web API 接口参考](https://developer.mozilla.org/zh-CN/docs/Web/API)
- [JavaScript.info - Web API](https://javascript.info/browser-environment)

了解和掌握 Web API 是前端开发的重要组成部分，它们为开发者提供了丰富的功能，可以创建更加交互和动态的网页应用。通过合理使用 Web API，可以提高网页的性能、安全性和用户体验。