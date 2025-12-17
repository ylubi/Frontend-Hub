# Rollup 核心概念

## 1. Rollup 基础

### 1.1 什么是 Rollup

Rollup 是一个 JavaScript 模块打包器，专注于构建 JavaScript 库和应用程序。与 Webpack 相比，Rollup 更加轻量、快速，并且生成的代码更加简洁高效。Rollup 优先支持 ES 模块，同时也可以通过插件支持 CommonJS 模块。

### 1.2 Rollup 的核心优势

1. **Tree Shaking**：自动移除未使用的代码，生成更小的 bundle
2. **简洁的输出**：生成的代码更加简洁，没有多余的运行时代码
3. **原生 ES 模块支持**：优先支持 ES 模块，同时兼容 CommonJS
4. **插件生态**：丰富的插件系统，可扩展各种功能
5. **快速构建**：构建速度快，适合中小型项目和库开发

### 1.3 Rollup 与 Webpack 的对比

| 特性 | Rollup | Webpack |
|------|--------|---------|
| 主要用途 | 库开发，小型应用 | 大型复杂应用 |
| Tree Shaking | 优秀 | 良好 |
| 输出代码 | 简洁，无多余运行时代码 | 包含运行时代码 |
| 模块支持 | 优先 ES 模块，兼容 CommonJS | 支持多种模块格式 |
| 构建速度 | 快 | 相对较慢 |
| 配置复杂度 | 简单 | 复杂 |
| 插件生态 | 丰富，专注于库开发 | 极其丰富，覆盖各种场景 |
| 热更新支持 | 有限 | 优秀 |
| 代码分割 | 支持，但不如 Webpack 灵活 | 强大，支持多种分割策略 |

## 2. Rollup 配置

### 2.1 基本配置

```javascript
// rollup.config.js
export default {
  input: 'src/index.js', // 入口文件
  output: {
    file: 'dist/bundle.js', // 输出文件
    format: 'es', // 输出格式
  },
};
```

### 2.2 多入口配置

```javascript
// rollup.config.js
export default {
  input: {
    main: 'src/index.js',
    vendor: 'src/vendor.js',
  },
  output: {
    dir: 'dist',
    format: 'es',
  },
};
```

### 2.3 多输出配置

```javascript
// rollup.config.js
export default {
  input: 'src/index.js',
  output: [
    {
      file: 'dist/bundle.es.js',
      format: 'es',
    },
    {
      file: 'dist/bundle.cjs.js',
      format: 'cjs',
    },
    {
      file: 'dist/bundle.umd.js',
      format: 'umd',
      name: 'MyLibrary', // UMD 模块名称
    },
  ],
};
```

## 3. Rollup 输出格式

### 3.1 常用输出格式

| 格式 | 名称 | 用途 | 适用场景 |
|------|------|------|----------|
| es | ES Module | ES 模块格式 | 现代浏览器，支持 ES 模块的环境 |
| cjs | CommonJS | CommonJS 模块格式 | Node.js 环境 |
| umd | Universal Module Definition | 通用模块定义，兼容 AMD、CommonJS 和全局变量 | 浏览器和 Node.js 通用 |
| amd | Asynchronous Module Definition | AMD 模块格式 | 浏览器环境，使用 RequireJS 等加载器 |
| iife | Immediately Invoked Function Expression | 立即执行函数表达式 | 浏览器环境，作为全局变量使用 |
| system | SystemJS | SystemJS 模块格式 | 使用 SystemJS 加载器的环境 |

### 3.2 输出格式配置示例

```javascript
// rollup.config.js
export default {
  input: 'src/index.js',
  output: {
    file: 'dist/bundle.js',
    format: 'es', // 输出为 ES 模块
    sourcemap: true, // 生成 source map
    name: 'MyLibrary', // 全局变量名称（UMD/iife 格式需要）
    globals: {
      react: 'React', // 外部依赖的全局变量名称
    },
  },
};
```

## 4. Rollup 插件

### 4.1 插件系统

Rollup 的插件系统基于钩子（hooks）机制，插件可以在构建过程的不同阶段介入，执行各种任务。Rollup 插件通常遵循 `rollup-plugin-*` 的命名约定。

### 4.2 常用插件

| 插件 | 用途 | 安装命令 |
|------|------|----------|
| @rollup/plugin-node-resolve | 解析 Node.js 模块 | `npm install @rollup/plugin-node-resolve` |
| @rollup/plugin-commonjs | 将 CommonJS 转换为 ES 模块 | `npm install @rollup/plugin-commonjs` |
| @rollup/plugin-babel | 使用 Babel 转换代码 | `npm install @rollup/plugin-babel` |
| @rollup/plugin-terser | 压缩 JavaScript | `npm install @rollup/plugin-terser` |
| @rollup/plugin-typescript | 处理 TypeScript 文件 | `npm install @rollup/plugin-typescript` |
| rollup-plugin-postcss | 处理 CSS 文件 | `npm install rollup-plugin-postcss` |
| rollup-plugin-vue | 处理 Vue 组件 | `npm install rollup-plugin-vue` |
| rollup-plugin-replace | 替换代码中的变量 | `npm install rollup-plugin-replace` |
| rollup-plugin-json | 处理 JSON 文件 | `npm install @rollup/plugin-json` |
| rollup-plugin-image | 处理图像文件 | `npm install rollup-plugin-image` |

### 4.3 插件配置示例

```javascript
// rollup.config.js
import resolve from '@rollup/plugin-node-resolve';
import commonjs from '@rollup/plugin-commonjs';
import babel from '@rollup/plugin-babel';
import terser from '@rollup/plugin-terser';
import typescript from '@rollup/plugin-typescript';
import postcss from 'rollup-plugin-postcss';

const production = process.env.NODE_ENV === 'production';

export default {
  input: 'src/index.js',
  output: {
    file: 'dist/bundle.js',
    format: 'es',
    sourcemap: !production,
  },
  plugins: [
    resolve(), // 解析 Node.js 模块
    commonjs(), // 转换 CommonJS 为 ES 模块
    typescript(), // 处理 TypeScript
    postcss({
      extensions: ['.css'],
      extract: true, // 提取 CSS 到单独文件
      minimize: production, // 生产环境压缩 CSS
    }),
    babel({
      exclude: 'node_modules/**',
      babelHelpers: 'bundled',
    }),
    production && terser(), // 生产环境压缩 JavaScript
  ],
};
```

## 5. Rollup 高级功能

### 5.1 Tree Shaking

Tree Shaking 是 Rollup 的核心特性，它能够自动移除未使用的代码，生成更小的 bundle。Tree Shaking 基于 ES 模块的静态分析特性，只能作用于 ES 模块。

#### 5.1.1 启用 Tree Shaking

在 Rollup 中，Tree Shaking 默认启用，无需额外配置。为了确保 Tree Shaking 正常工作，需要注意以下几点：

1. 使用 ES 模块语法（import/export）
2. 避免使用 `eval()`、`Function()` 等动态代码
3. 避免修改全局对象
4. 生产环境构建时，确保代码被压缩

#### 5.1.2 Tree Shaking 示例

```javascript
// src/utils.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// src/index.js
import { add } from './utils.js'; // 只导入 add 函数

console.log(add(1, 2)); // 只使用 add 函数

// 构建结果（Tree Shaking 后）
const add = (a, b) => a + b;

console.log(add(1, 2));
// subtract 函数被自动移除
```

### 5.2 代码分割

Rollup 支持代码分割，允许将代码分割成多个 chunk，实现按需加载。

#### 5.2.1 动态导入

使用动态导入（dynamic import）是实现代码分割的主要方式：

```javascript
// src/index.js
button.addEventListener('click', async () => {
  const module = await import('./module.js');
  module.doSomething();
});
```

#### 5.2.2 代码分割配置

```javascript
// rollup.config.js
export default {
  input: 'src/index.js',
  output: {
    dir: 'dist', // 必须使用 dir 而不是 file
    format: 'es', // 代码分割只支持 es 和 system 格式
    sourcemap: true,
  },
};
```

### 5.3 外部依赖

在构建库时，通常需要将某些依赖标记为外部依赖，避免将它们打包到最终的 bundle 中。

```javascript
// rollup.config.js
export default {
  input: 'src/index.js',
  output: {
    file: 'dist/bundle.js',
    format: 'umd',
    name: 'MyLibrary',
    globals: {
      react: 'React', // 外部依赖的全局变量名称
      'react-dom': 'ReactDOM',
    },
  },
  external: ['react', 'react-dom'], // 标记为外部依赖
};
```

## 6. Rollup 与框架集成

### 6.1 React 集成

```javascript
// rollup.config.js
import resolve from '@rollup/plugin-node-resolve';
import commonjs from '@rollup/plugin-commonjs';
import babel from '@rollup/plugin-babel';
import typescript from '@rollup/plugin-typescript';

export default {
  input: 'src/index.jsx',
  output: {
    file: 'dist/bundle.js',
    format: 'es',
  },
  plugins: [
    resolve(),
    commonjs(),
    typescript({
      tsconfig: './tsconfig.json',
    }),
    babel({
      exclude: 'node_modules/**',
      presets: ['@babel/preset-react'],
      babelHelpers: 'bundled',
    }),
  ],
  external: ['react', 'react-dom'],
};
```

### 6.2 Vue 集成

```javascript
// rollup.config.js
import resolve from '@rollup/plugin-node-resolve';
import commonjs from '@rollup/plugin-commonjs';
import vue from 'rollup-plugin-vue';
import postcss from 'rollup-plugin-postcss';

export default {
  input: 'src/index.js',
  output: {
    file: 'dist/bundle.js',
    format: 'es',
  },
  plugins: [
    resolve(),
    commonjs(),
    vue({
      css: false, // 禁用 Vue 组件内联 CSS，使用 postcss 处理
    }),
    postcss({
      extensions: ['.css', '.scss'],
      extract: true,
    }),
  ],
};
```

### 6.3 TypeScript 集成

```javascript
// rollup.config.js
import resolve from '@rollup/plugin-node-resolve';
import commonjs from '@rollup/plugin-commonjs';
import typescript from '@rollup/plugin-typescript';

export default {
  input: 'src/index.ts',
  output: {
    file: 'dist/bundle.js',
    format: 'es',
  },
  plugins: [
    resolve(),
    commonjs(),
    typescript({
      tsconfig: './tsconfig.json',
      declaration: true, // 生成类型声明文件
      declarationDir: 'dist/types', // 类型声明文件输出目录
    }),
  ],
};
```

## 7. Rollup 最佳实践

### 7.1 库开发最佳实践

1. **使用 ES 模块**：优先使用 ES 模块语法，确保 Tree Shaking 正常工作
2. **多格式输出**：同时输出 ES 模块和 CommonJS 格式，方便不同环境使用
3. **生成类型声明**：使用 TypeScript 或 JSDoc 生成类型声明文件
4. **标记外部依赖**：将第三方依赖标记为外部依赖，避免打包到最终产物
5. **使用插件压缩代码**：生产环境使用 terser 压缩代码
6. **生成 source map**：方便调试

### 7.2 应用开发最佳实践

1. **使用代码分割**：将代码分割成多个 chunk，优化加载性能
2. **使用动态导入**：按需加载不常用的功能
3. **集成 Babel**：确保代码兼容目标环境
4. **处理静态资源**：使用合适的插件处理 CSS、图像等静态资源
5. **配置环境变量**：使用 rollup-plugin-replace 配置不同环境的变量

### 7.3 配置文件最佳实践

1. **分离开发和生产配置**：使用环境变量或不同的配置文件
2. **使用插件组合**：合理组合插件，实现所需功能
3. **注释配置项**：为复杂的配置项添加注释
4. **使用 ESM 配置**：优先使用 ESM 格式的配置文件

## 8. Rollup 生态系统

### 8.1 常用工具

| 工具 | 用途 |
|------|------|
| rollup | Rollup 核心包 |
| rollup-plugin-serve | 开发服务器 |
| rollup-plugin-livereload | 热重载 |
| @rollup/plugin-watch | 文件监听 |
| rollup-plugin-analyzer | 分析 bundle 大小 |
| rollup-plugin-visualizer | 可视化 bundle 结构 |

### 8.2 替代方案

| 工具 | 优势 | 适用场景 |
|------|------|----------|
| Webpack | 强大的代码分割，丰富的插件生态 | 大型复杂应用 |
| Vite | 极快的启动速度，按需编译 | 现代前端项目 |
| Parcel | 零配置，快速上手 | 小型项目，快速原型开发 |
| Esbuild | 极快的构建速度 | 需要快速构建的项目 |

## 9. 总结

Rollup 是一个优秀的 JavaScript 模块打包器，特别适合构建 JavaScript 库和中小型应用。它的核心优势是 Tree Shaking 和简洁的输出代码，能够生成更小、更高效的 bundle。

虽然 Rollup 在某些方面（如代码分割、热更新）不如 Webpack 强大，但对于库开发和中小型应用来说，Rollup 是一个更加轻量、快速的选择。

了解 Rollup 的核心概念和最佳实践，能够帮助前端开发者更好地配置和使用 Rollup，优化项目的构建流程和性能。