# 前端知识树状结构

## 1. 基础核心

### 1.1 HTML
- 基本概念
- 文档结构
- 常用标签
  - 语义化标签
  - 表单标签
  - 媒体标签
- HTML5 新特性
  - Canvas
  - SVG
  - Web Storage
  - Web Workers
  - WebSockets
- HTML 最佳实践

### 1.2 CSS
- 基础语法
- 选择器
  - 基本选择器
  - 组合选择器
  - 伪类/伪元素
  - 属性选择器
- 盒模型
- 布局
  - Flexbox
  - Grid
  - 定位
  - 浮动
  - 多列布局
- 样式
  - 颜色与单位
  - 字体与文本
  - 背景与边框
  - 阴影与渐变
  - 变换与过渡
  - 动画
- CSS 预处理器
  - Sass/SCSS
  - Less
  - Stylus
- CSS 模块化
- CSS-in-JS
- CSS 架构
  - BEM
  - OOCSS
  - SMACSS
  - ITCSS
- CSS 最佳实践

### 1.3 JavaScript
- 语言基础
  - 数据类型
  - 运算符
  - 流程控制
  - 函数
  - 对象
  - 数组
  - 字符串
- 高级特性
  - 原型与原型链
  - 闭包
  - this 指向
  - 异步编程
    - 回调函数
    - Promise
    - async/await
  - 事件循环
  - 模块化
    - CommonJS
    - ES Modules
  - 设计模式
- DOM 操作
- BOM
- 正则表达式
- JavaScript 最佳实践

### 1.4 TypeScript
- 基础语法
- 类型系统
  - 基本类型
  - 高级类型
  - 泛型
  - 接口
  - 类型别名
  - 枚举
- 编译配置
- 高级特性
  - 装饰器
  - 命名空间
  - 声明文件
- TypeScript 最佳实践

## 2. 框架与库

### 2.1 React
- [核心概念](index.html?file=frameworks/react/core-concepts.md)
  - JSX
  - 组件
  - Props
  - State
  - 生命周期
  - Hooks
    - useState
    - useEffect
    - useContext
    - useReducer
    - useCallback
    - useMemo
    - useRef
    - 自定义 Hooks
- 进阶特性
  - Context API
  - 高阶组件
  - Render Props
  - Suspense
  - Lazy Loading
- React 生态
  - React Router
  - Redux
  - MobX
  - Zustand
  - React Query
  - Axios
- React 最佳实践
- Next.js

### 2.2 Vue
- [核心概念](index.html?file=frameworks/vue/core-concepts.md)
- Vue 2 vs Vue 3
  - 模板语法
  - 组件
  - Props
  - Data/Methods
  - 生命周期
  - Computed/Watch
  - 指令
  - 事件处理
- 进阶特性
  - 组件通信
  - 插槽
  - 混入
  - 插件
- Composition API
  - setup 函数
  - 响应式系统
  - 组合式函数
- Vue 生态
  - Vue Router
  - Vuex
  - Pinia
  - Axios
  - VueUse
- Vue 最佳实践
- Nuxt.js

### 2.3 Angular
- [核心概念](index.html?file=frameworks/angular/core-concepts.md)
  - 组件
  - 模板
  - 指令
  - 服务
  - 依赖注入
  - 模块
- 进阶特性
  - 路由
  - 表单
  - HTTP 客户端
  - 状态管理
  - 动画
- Angular 最佳实践
- Angular CLI

### 2.4 Svelte
- [核心概念](index.html?file=frameworks/svelte/core-concepts.md)
- 响应式系统
- 组件
- 状态管理
- SvelteKit
- Svelte 最佳实践

### 2.5 其他流行库
- jQuery
- Lodash/Underscore
- Moment.js/Date-fns/Day.js
- Axios
- Chart.js/ECharts
- Three.js
- D3.js

## 3. 工程化

### 3.1 构建工具
- [Webpack](index.html?file=engineering/build-tools/webpack/core-concepts.md)
- [Vite](index.html?file=engineering/build-tools/vite/core-concepts.md)
- [Rollup](index.html?file=engineering/build-tools/rollup/core-concepts.md)
- [Parcel](index.html?file=engineering/build-tools/parcel/core-concepts.md)
- [Esbuild](index.html?file=engineering/build-tools/esbuild/core-concepts.md)

### 3.2 包管理
- [npm](index.html?file=engineering/package-management/npm/core-concepts.md)
- [Yarn](index.html?file=engineering/package-management/yarn/core-concepts.md)
- [pnpm](index.html?file=engineering/package-management/pnpm/core-concepts.md)

### 3.3 代码规范
- [ESLint](index.html?file=engineering/code-standards/core-concepts.md)
- [Prettier](index.html?file=engineering/code-standards/core-concepts.md)
- [Stylelint](index.html?file=engineering/code-standards/core-concepts.md)
- [Husky](index.html?file=engineering/code-standards/core-concepts.md)
- [Lint-staged](index.html?file=engineering/code-standards/core-concepts.md)

### 3.4 CI/CD
- [GitHub Actions](index.html?file=engineering/ci-cd/core-concepts.md)
- [GitLab CI](index.html?file=engineering/ci-cd/core-concepts.md)
- [Jenkins](index.html?file=engineering/ci-cd/core-concepts.md)
- [CircleCI](index.html?file=engineering/ci-cd/core-concepts.md)

### 3.5 开发环境
- [VS Code 配置](index.html?file=engineering/development-environment/core-concepts.md)
- [Chrome DevTools](index.html?file=engineering/development-environment/core-concepts.md)
- [调试技巧](index.html?file=engineering/development-environment/core-concepts.md)
- [热更新](index.html?file=engineering/development-environment/core-concepts.md)
- [Mock 数据](index.html?file=engineering/development-environment/core-concepts.md)

## 4. 性能优化

### 4.1 加载优化
- [资源压缩](index.html?file=performance-optimization/loading-optimization/core-concepts.md)
- [代码分割](index.html?file=performance-optimization/loading-optimization/core-concepts.md)
- [懒加载](index.html?file=performance-optimization/loading-optimization/core-concepts.md)
- [预加载/预连接](index.html?file=performance-optimization/loading-optimization/core-concepts.md)
- [CDN 加速](index.html?file=performance-optimization/loading-optimization/core-concepts.md)
- [缓存策略](index.html?file=performance-optimization/loading-optimization/core-concepts.md)

### 4.2 渲染优化
- [CSS 优化](index.html?file=performance-optimization/rendering-optimization/core-concepts.md)
- [JavaScript 执行优化](index.html?file=performance-optimization/rendering-optimization/core-concepts.md)
- [减少重排重绘](index.html?file=performance-optimization/rendering-optimization/core-concepts.md)
- [虚拟列表](index.html?file=performance-optimization/rendering-optimization/core-concepts.md)
- [骨架屏](index.html?file=performance-optimization/rendering-optimization/core-concepts.md)

### 4.3 运行时优化
- [内存管理](index.html?file=performance-optimization/runtime-optimization/core-concepts.md)
- [事件委托](index.html?file=performance-optimization/runtime-optimization/core-concepts.md)
- [Web Workers](index.html?file=performance-optimization/runtime-optimization/core-concepts.md)
- [防抖节流](index.html?file=performance-optimization/runtime-optimization/core-concepts.md)

### 4.4 性能监控
- [Lighthouse](index.html?file=performance-optimization/performance-monitoring/core-concepts.md)
- [Performance API](index.html?file=performance-optimization/performance-monitoring/core-concepts.md)
- [第三方监控工具](index.html?file=performance-optimization/performance-monitoring/core-concepts.md)

## 5. 浏览器与网络

### 5.1 浏览器原理
- [浏览器架构](index.html?file=browser-network/browser-principles/core-concepts.md)
- [渲染流程](index.html?file=browser-network/browser-principles/core-concepts.md)
- [JavaScript 引擎](index.html?file=browser-network/browser-principles/core-concepts.md)
- [事件循环](index.html?file=browser-network/browser-principles/core-concepts.md)
- [存储机制](index.html?file=browser-network/browser-principles/core-concepts.md)

### 5.2 HTTP 协议
- [HTTP 基础](index.html?file=browser-network/http-protocol/core-concepts.md)
- [HTTP/1.1 vs HTTP/2 vs HTTP/3](index.html?file=browser-network/http-protocol/core-concepts.md)
- [HTTPS](index.html?file=browser-network/http-protocol/core-concepts.md)
- [RESTful API](index.html?file=browser-network/http-protocol/core-concepts.md)
- [GraphQL](index.html?file=browser-network/http-protocol/core-concepts.md)
- [WebSocket](index.html?file=browser-network/http-protocol/core-concepts.md)

### 5.3 Web API
- [DOM API](index.html?file=browser-network/web-api/core-concepts.md)
- [BOM API](index.html?file=browser-network/web-api/core-concepts.md)
- [Fetch API](browser-network/web-api/core-concepts.md)
- [Web Storage API](index.html?file=browser-network/web-api/core-concepts.md)
- [IndexedDB](index.html?file=browser-network/web-api/core-concepts.md)
- [Web Audio API](index.html?file=browser-network/web-api/core-concepts.md)
- [Web Speech API](index.html?file=browser-network/web-api/core-concepts.md)
- [WebXR API](index.html?file=browser-network/web-api/core-concepts.md)

### 5.4 浏览器兼容性
- [兼容性处理策略](index.html?file=browser-network/browser-compatibility/core-concepts.md)
- [Polyfill](index.html?file=browser-network/browser-compatibility/core-concepts.md)
- [降级方案](index.html?file=browser-network/browser-compatibility/core-concepts.md)
- [浏览器市场份额](index.html?file=browser-network/browser-compatibility/core-concepts.md)

## 6. 设计与用户体验

### 6.1 UI 设计原则
- [色彩理论](index.html?file=design-ux/ui-design-principles/core-concepts.md)
- [排版设计](index.html?file=design-ux/ui-design-principles/core-concepts.md)
- [视觉层次](index.html?file=design-ux/ui-design-principles/core-concepts.md)
- [一致性](index.html?file=design-ux/ui-design-principles/core-concepts.md)
- [简洁性](index.html?file=design-ux/ui-design-principles/core-concepts.md)

### 6.2 交互设计
- [用户研究](index.html?file=design-ux/interaction-design/core-concepts.md)
- [交互模式](index.html?file=design-ux/interaction-design/core-concepts.md)
- [反馈机制](index.html?file=design-ux/interaction-design/core-concepts.md)
- [微交互](index.html?file=design-ux/interaction-design/core-concepts.md)

### 6.3 响应式设计
- [媒体查询](index.html?file=design-ux/responsive-design/core-concepts.md)
- [流体布局](index.html?file=design-ux/responsive-design/core-concepts.md)
- [弹性图片](index.html?file=design-ux/responsive-design/core-concepts.md)
- [移动端适配](index.html?file=design-ux/responsive-design/core-concepts.md)

### 6.4 无障碍设计
- [ARIA 规范](index.html?file=design-ux/accessibility/core-concepts.md)
- [键盘导航](index.html?file=design-ux/accessibility/core-concepts.md)
- [屏幕阅读器支持](index.html?file=design-ux/accessibility/core-concepts.md)
- [对比度要求](index.html?file=design-ux/accessibility/core-concepts.md)

### 6.5 设计系统
- [设计 tokens](index.html?file=design-ux/design-system/core-concepts.md)
- [组件库](index.html?file=design-ux/design-system/core-concepts.md)
- [设计规范](index.html?file=design-ux/design-system/core-concepts.md)

## 7. 测试与质量保障

### 7.1 单元测试
- 测试框架
  - [Jest](index.html?file=testing-quality/unit-testing/core-concepts.md)
  - [Mocha](index.html?file=testing-quality/unit-testing/core-concepts.md)
  - [Vitest](index.html?file=testing-quality/unit-testing/core-concepts.md)
- 断言库
  - Chai
  - Assert
- [测试覆盖率](index.html?file=testing-quality/unit-testing/core-concepts.md)

### 7.2 集成测试
- [React Testing Library](index.html?file=testing-quality/integration-testing/core-concepts.md)
- [Vue Test Utils](index.html?file=testing-quality/integration-testing/core-concepts.md)
- [Cypress Component Testing](index.html?file=testing-quality/integration-testing/core-concepts.md)

### 7.3 E2E 测试
- [Cypress](index.html?file=testing-quality/e2e-testing/core-concepts.md)
- [Playwright](index.html?file=testing-quality/e2e-testing/core-concepts.md)
- [Puppeteer](index.html?file=testing-quality/e2e-testing/core-concepts.md)

### 7.4 测试工具
- Testing Library
- Sinon
- Mock Service Worker

### 7.5 代码质量
- 代码审查
- 静态分析
- 复杂度分析

## 8. 跨端开发

### 8.1 移动端开发
- [响应式设计](index.html?file=cross-platform/mobile-development/core-concepts.md)
- [移动端适配](cross-platform/mobile-development/core-concepts.md)
- [PWA](cross-platform/mobile-development/core-concepts.md)
- [TWA](cross-platform/mobile-development/core-concepts.md)

### 8.2 桌面端开发
- [Electron](cross-platform/desktop-development/core-concepts.md)
- [NW.js](cross-platform/desktop-development/core-concepts.md)
- [Tauri](cross-platform/desktop-development/core-concepts.md)

### 8.3 小程序开发
- [微信小程序](cross-platform/miniprogram-development/core-concepts.md)
- [支付宝小程序](cross-platform/miniprogram-development/core-concepts.md)
- [百度小程序](cross-platform/miniprogram-development/core-concepts.md)
- [跨平台小程序框架](cross-platform/miniprogram-development/core-concepts.md)
  - Taro
  - Uni-app

### 8.4 WebAssembly
- [基本概念](cross-platform/webassembly/core-concepts.md)
- [使用场景](cross-platform/webassembly/core-concepts.md)
- [编译工具](cross-platform/webassembly/core-concepts.md)
  - Emscripten
  - Rust + Wasm

## 9. 安全

### 9.1 Web 安全基础
- [同源策略](security/web-security-basics/core-concepts.md)
- [CORS](security/web-security-basics/core-concepts.md)
- [CSP](security/web-security-basics/core-concepts.md)

### 9.2 XSS 防护
- [反射型 XSS](security/xss-protection/core-concepts.md)
- [存储型 XSS](security/xss-protection/core-concepts.md)
- [DOM 型 XSS](security/xss-protection/core-concepts.md)
- [防护措施](security/xss-protection/core-concepts.md)

### 9.3 CSRF 防护
- [攻击原理](security/csrf-protection/core-concepts.md)
- [防护措施](security/csrf-protection/core-concepts.md)

### 9.4 数据安全
- [数据加密](security/data-security/core-concepts.md)
- [敏感数据处理](security/data-security/core-concepts.md)
- [隐私保护](security/data-security/core-concepts.md)

### 9.5 身份验证与授权
- [Cookie/Session](security/authentication-authorization/core-concepts.md)
- [JWT](security/authentication-authorization/core-concepts.md)
- [OAuth 2.0](security/authentication-authorization/core-concepts.md)
- [OpenID Connect](security/authentication-authorization/core-concepts.md)
- [生物识别认证](security/authentication-authorization/core-concepts.md)

## 10. 高级概念

### 10.1 微前端
- [概念与架构](advanced-concepts/micro-frontends/core-concepts.md)
- [实现方案](advanced-concepts/micro-frontends/core-concepts.md)
  - Module Federation
  - Single-SPA
  - Qiankun
- [微前端最佳实践](advanced-concepts/micro-frontends/core-concepts.md)

### 10.2 服务端渲染
- [SSR 概念](advanced-concepts/server-side-rendering/core-concepts.md)
- [Next.js](advanced-concepts/server-side-rendering/core-concepts.md)
- [Nuxt.js](advanced-concepts/server-side-rendering/core-concepts.md)
- [Angular Universal](advanced-concepts/server-side-rendering/core-concepts.md)
- [SSR 最佳实践](advanced-concepts/server-side-rendering/core-concepts.md)

### 10.3 静态站点生成
- [SSG 概念](advanced-concepts/static-site-generation/core-concepts.md)
- [Next.js (SSG)](advanced-concepts/static-site-generation/core-concepts.md)
- [Nuxt.js (SSG)](advanced-concepts/static-site-generation/core-concepts.md)
- [Astro](advanced-concepts/static-site-generation/core-concepts.md)
- [Gatsby](advanced-concepts/static-site-generation/core-concepts.md)
- [SSG 最佳实践](advanced-concepts/static-site-generation/core-concepts.md)

### 10.4 Web 3.0
- [区块链基础](advanced-concepts/web-3-0/core-concepts.md)
- [智能合约](advanced-concepts/web-3-0/core-concepts.md)
- [DApp 开发](advanced-concepts/web-3-0/core-concepts.md)
- [Web3.js/Ethers.js](advanced-concepts/web-3-0/core-concepts.md)
- [NFT 与元宇宙](advanced-concepts/web-3-0/core-concepts.md)

### 10.5 AI 与前端结合
- [AI 图像生成](advanced-concepts/ai-integration/core-concepts.md)
- [AI 代码生成](advanced-concepts/ai-integration/core-concepts.md)
- [智能交互](advanced-concepts/ai-integration/core-concepts.md)
- [机器学习在前端的应用](advanced-concepts/ai-integration/core-concepts.md)
- [大语言模型集成](advanced-concepts/ai-integration/core-concepts.md)
