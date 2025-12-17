# Vite 核心概念

## 目录

- [什么是 Vite](#什么是-vite)
- [Vite 的特点](#vite-的特点)
- [Vite 与其他构建工具的比较](#vite-与其他构建工具的比较)
- [Vite 核心概念](#vite-核心概念)
  - [开发服务器](#开发服务器)
  - [构建系统](#构建系统)
  - [插件系统](#插件系统)
  - [依赖预构建](#依赖预构建)
  - [ES 模块](#es-模块)
  - [HMR（热模块替换）](#hmr热模块替换)
  - [配置文件](#配置文件)
- [Vite 项目结构](#vite-项目结构)
- [Vite 配置](#vite-配置)
  - [基本配置](#基本配置)
  - [开发服务器配置](#开发服务器配置)
  - [构建配置](#构建配置)
  - [插件配置](#插件配置)
  - [环境变量](#环境变量)
- [Vite 插件](#vite-插件)
  - [常用插件](#常用插件)
  - [自定义插件](#自定义插件)
- [Vite 与框架集成](#vite-与框架集成)
  - [React](#react)
  - [Vue](#vue)
  - [Svelte](#svelte)
- [Vite 最佳实践](#vite-最佳实践)
- [参考资源](#参考资源)

## 什么是 Vite

Vite（法语意为 "快速"）是下一代前端构建工具，由 Vue.js 的作者尤雨溪开发。它基于浏览器原生 ES 模块系统，提供了极速的开发体验和优异的构建性能。

Vite 主要解决了传统构建工具（如 Webpack）在大型项目中的性能瓶颈问题，通过使用原生 ES 模块和预构建依赖，实现了秒级的热更新和快速的构建速度。

## Vite 的特点

1. **极速的开发服务器**：基于原生 ES 模块，无需打包，启动速度快
2. **快速的热模块替换**：HMR 性能优异，支持多种框架
3. **优化的构建过程**：使用 Rollup 进行生产构建，生成高度优化的静态资源
4. **支持多种框架**：内置支持 React、Vue、Svelte 等主流框架
5. **强大的插件系统**：基于 Rollup 插件 API，生态丰富
6. **TypeScript 支持**：内置 TypeScript 支持，无需额外配置
7. **CSS 支持**：支持 CSS Modules、CSS 预处理器、CSS-in-JS
8. **优化的依赖预构建**：使用 esbuild 预构建依赖，提高加载速度
9. **环境变量支持**：内置环境变量处理
10. **API 友好**：提供了丰富的 API，便于自定义配置

## Vite 与其他构建工具的比较

| 特性 | Vite | Webpack | Rollup | Parcel |
|------|------|---------|--------|--------|
| 类型 | 构建工具 | 构建工具 | 模块打包器 | 构建工具 |
| 开发服务器 | 极速（基于 ES 模块） | 较慢（需要打包） | 无内置 | 较快 |
| HMR 性能 | 优异 | 良好 | 无内置 | 良好 |
| 生产构建 | 基于 Rollup，优化良好 | 内置，配置复杂 | 原生，优化优异 | 内置，配置简单 |
| 配置复杂度 | 简单 | 复杂 | 中等 | 简单 |
| 插件生态 | 正在快速发展 | 成熟 | 成熟 | 中等 |
| TypeScript 支持 | 内置 | 需要配置 | 需要配置 | 内置 |
| 适合项目 | 各种规模，尤其适合大型项目 | 各种规模 | 库和框架 | 各种规模 |
| 启动时间 | 秒级 | 分钟级（大型项目） | - | 秒级 |

## Vite 核心概念

### 开发服务器

Vite 的开发服务器基于原生 ES 模块，无需在开发过程中打包所有文件，而是按需提供文件，从而实现了极速的启动速度和热更新。

#### 工作原理

1. 当浏览器请求一个模块时，Vite 服务器会拦截请求
2. 如果是 npm 依赖，Vite 会返回预构建后的 ES 模块
3. 如果是项目源码，Vite 会实时编译并返回编译后的结果
4. 支持热模块替换，修改文件后只更新变化的部分

### 构建系统

Vite 使用 Rollup 进行生产构建，生成高度优化的静态资源。

#### 构建特点

1. **代码分割**：自动进行代码分割，优化加载性能
2. **Tree Shaking**：移除未使用的代码
3. **CSS 处理**：优化 CSS，支持 CSS Modules
4. **资源优化**：压缩图片、字体等资源
5. **动态导入**：支持动态导入，实现按需加载

### 插件系统

Vite 插件系统基于 Rollup 插件 API，但提供了一些 Vite 特有的钩子，以便于处理开发服务器相关的逻辑。

#### 插件类型

1. **通用插件**：同时用于开发和构建
2. **构建插件**：只用于生产构建
3. **虚拟模块插件**：创建虚拟模块
4. **转换插件**：转换文件内容

### 依赖预构建

Vite 会在首次启动时预构建 npm 依赖，将 CommonJS 或 UMD 格式的依赖转换为 ES 模块，并缓存结果。

#### 预构建的好处

1. **提高加载速度**：减少网络请求次数
2. **支持 CommonJS 依赖**：将 CommonJS 依赖转换为 ES 模块
3. **缓存机制**：只在依赖变化时重新构建
4. **减少浏览器兼容性问题**：处理依赖中的兼容性问题

### ES 模块

Vite 基于浏览器原生 ES 模块系统，使用 `import` 和 `export` 语法。

#### ES 模块的优势

1. **原生支持**：现代浏览器原生支持 ES 模块
2. **按需加载**：浏览器可以按需加载模块
3. **静态分析**：便于工具进行静态分析和优化
4. **更好的性能**：减少运行时开销

### HMR（热模块替换）

Vite 提供了快速的热模块替换功能，修改文件后只更新变化的部分，无需刷新整个页面。

#### HMR 特点

1. **极速响应**：修改文件后立即更新
2. **状态保持**：保留组件状态，提高开发效率
3. **框架支持**：内置支持 React、Vue、Svelte 等框架
4. **自定义 HMR**：支持自定义 HMR 逻辑

### 配置文件

Vite 使用 `vite.config.js` 或 `vite.config.ts` 作为配置文件。

#### 配置文件示例

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
    open: true
  },
  build: {
    outDir: 'dist',
    sourcemap: true
  }
});
```

## Vite 项目结构

```
vite-project/
├── src/                # 源代码目录
│   ├── assets/         # 静态资源
│   ├── components/     # 组件
│   ├── App.jsx         # 根组件
│   └── main.jsx        # 入口文件
├── public/             # 公共资源目录
│   └── favicon.ico     # 网站图标
├── vite.config.js      # Vite 配置文件
├── package.json        # 项目依赖
└── index.html          # HTML 模板
```

## Vite 配置

### 基本配置

```javascript
// vite.config.js
import { defineConfig } from 'vite';

export default defineConfig({
  // 项目根目录
  root: '.',
  // 公共基础路径
  base: '/',
  // 模式
  mode: 'development',
  // 插件配置
  plugins: [],
  // 解析配置
  resolve: {
    // 别名配置
    alias: {
      '@': '/src'
    },
    // 扩展名列表
    extensions: ['.mjs', '.js', '.ts', '.jsx', '.tsx', '.json']
  }
});
```

### 开发服务器配置

```javascript
// vite.config.js
import { defineConfig } from 'vite';

export default defineConfig({
  server: {
    // 端口
    port: 3000,
    // 是否自动打开浏览器
    open: true,
    // 是否启用 https
    https: false,
    // 代理配置
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '')
      }
    },
    // 服务器主机名
    host: 'localhost',
    // 热更新配置
    hmr: {
      overlay: true
    },
    // 中间件配置
    middlewareMode: false
  }
});
```

### 构建配置

```javascript
// vite.config.js
import { defineConfig } from 'vite';

export default defineConfig({
  build: {
    // 输出目录
    outDir: 'dist',
    // 静态资源目录
    assetsDir: 'assets',
    // 生成 sourcemap
    sourcemap: false,
    // 代码分割策略
    rollupOptions: {
      output: {
        manualChunks: {
          'vendor': ['react', 'react-dom'],
          'utils': ['lodash']
        }
      }
    },
    // 最小化配置
    minify: 'esbuild',
    // 生产环境下移除 console 和 debugger
    terserOptions: {
      compress: {
        drop_console: true,
        drop_debugger: true
      }
    },
    //  chunk 大小警告限制
    chunkSizeWarningLimit: 1000,
    // 是否生成 manifest.json
    manifest: false,
    // 是否启用 ssrManifest
    ssrManifest: false,
    // 是否为空目录生成占位文件
    emptyOutDir: true
  }
});
```

### 插件配置

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import vue from '@vitejs/plugin-vue';
import svelte from '@sveltejs/vite-plugin-svelte';
import { viteCommonjs } from '@originjs/vite-plugin-commonjs';
import { viteMockServe } from 'vite-plugin-mock';

export default defineConfig({
  plugins: [
    // 根据框架选择相应的插件
    react(),
    // vue(),
    // svelte(),
    
    // 其他插件
    viteCommonjs(),
    viteMockServe({
      mockPath: 'mock',
      enable: true
    })
  ]
});
```

### 环境变量

Vite 支持环境变量，使用 `.env` 文件定义。

#### 环境变量文件

```
.env                # 所有环境通用
.env.local          # 所有环境通用，不提交到 git
.env.development    # 开发环境
.env.production     # 生产环境
.env.test           # 测试环境
```

#### 环境变量使用

```javascript
// 在代码中使用环境变量
console.log(import.meta.env.VITE_API_URL);
console.log(import.meta.env.NODE_ENV);
console.log(import.meta.env.BASE_URL);
```

#### 环境变量配置

```javascript
// vite.config.js
import { defineConfig } from 'vite';

export default defineConfig({
  // 环境变量前缀
  envPrefix: 'VITE_',
  // 加载额外的环境变量文件
  envFile: '.env'
});
```

## Vite 插件

### 常用插件

1. **框架插件**：
   - `@vitejs/plugin-react`：React 支持
   - `@vitejs/plugin-vue`：Vue 支持
   - `@sveltejs/vite-plugin-svelte`：Svelte 支持

2. **TypeScript 插件**：
   - `@rollup/plugin-typescript`：TypeScript 支持
   - `vite-plugin-dts`：生成 TypeScript 声明文件

3. **CSS 插件**：
   - `vite-plugin-purgecss`：移除未使用的 CSS
   - `vite-plugin-windicss`：Windi CSS 支持

4. **资源插件**：
   - `vite-plugin-svg-icons`：SVG 图标支持
   - `vite-plugin-image-optimizer`：图片优化

5. **开发工具插件**：
   - `vite-plugin-mock`：Mock 数据支持
   - `vite-plugin-eslint`：ESLint 集成
   - `vite-plugin-pwa`：PWA 支持

### 自定义插件

```javascript
// my-plugin.js
import { createFilter } from '@rollup/pluginutils';

export default function myPlugin(options = {}) {
  const filter = createFilter(options.include || '**/*.js', options.exclude || 'node_modules/**');

  return {
    name: 'my-plugin',
    
    // 转换文件内容
    transform(code, id) {
      if (!filter(id)) return null;
      
      // 自定义转换逻辑
      return {
        code: code.replace(/console.log/g, ''),
        map: null
      };
    },
    
    // 生成额外的文件
    generateBundle(options, bundle) {
      // 自定义生成逻辑
    }
  };
}

// vite.config.js
import { defineConfig } from 'vite';
import myPlugin from './my-plugin';

export default defineConfig({
  plugins: [myPlugin()]
});
```

## Vite 与框架集成

### React

#### 快速开始

```bash
# 创建 React 项目
npm create vite@latest my-react-app -- --template react
# 或使用 TypeScript
npm create vite@latest my-react-app -- --template react-ts

# 安装依赖
cd my-react-app
npm install

# 启动开发服务器
npm run dev

# 构建生产版本
npm run build
```

#### React 配置示例

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [
    react({
      // React 插件配置
      jsxRuntime: 'automatic',
      babel: {
        plugins: [
          ['@babel/plugin-proposal-decorators', { legacy: true }]
        ]
      }
    })
  ],
  resolve: {
    alias: {
      '@': '/src'
    }
  }
});
```

### Vue

#### 快速开始

```bash
# 创建 Vue 项目
npm create vite@latest my-vue-app -- --template vue
# 或使用 TypeScript
npm create vite@latest my-vue-app -- --template vue-ts

# 安装依赖
cd my-vue-app
npm install

# 启动开发服务器
npm run dev

# 构建生产版本
npm run build
```

#### Vue 配置示例

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';

export default defineConfig({
  plugins: [
    vue({
      // Vue 插件配置
      script: {
        defineModel: true,
        propsDestructure: true
      }
    })
  ],
  resolve: {
    alias: {
      '@': '/src'
    }
  }
});
```

### Svelte

#### 快速开始

```bash
# 创建 Svelte 项目
npm create vite@latest my-svelte-app -- --template svelte
# 或使用 TypeScript
npm create vite@latest my-svelte-app -- --template svelte-ts

# 安装依赖
cd my-svelte-app
npm install

# 启动开发服务器
npm run dev

# 构建生产版本
npm run build
```

#### Svelte 配置示例

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import { svelte } from '@sveltejs/vite-plugin-svelte';

export default defineConfig({
  plugins: [
    svelte({
      // Svelte 插件配置
      compilerOptions: {
        dev: true
      },
      emitCss: true
    })
  ],
  resolve: {
    alias: {
      '@': '/src'
    }
  }
});
```

## Vite 最佳实践

1. **使用别名简化导入**：
   ```javascript
   // vite.config.js
   export default defineConfig({
     resolve: {
       alias: {
         '@': '/src'
       }
     }
   });
   ```

2. **合理配置代理**：
   ```javascript
   // vite.config.js
   export default defineConfig({
     server: {
       proxy: {
         '/api': {
           target: 'http://localhost:8080',
           changeOrigin: true
         }
       }
     }
   });
   ```

3. **优化构建配置**：
   ```javascript
   // vite.config.js
   export default defineConfig({
     build: {
       sourcemap: process.env.NODE_ENV !== 'production',
       rollupOptions: {
         output: {
           manualChunks: {
             'vendor': ['react', 'react-dom'],
             'utils': ['lodash']
           }
         }
       }
     }
   });
   ```

4. **使用环境变量**：
   ```javascript
   // .env.development
   VITE_API_URL=http://localhost:8080/api
   
   // .env.production
   VITE_API_URL=https://api.example.com
   ```

5. **优化依赖预构建**：
   ```javascript
   // vite.config.js
   export default defineConfig({
     optimizeDeps: {
       include: ['lodash', 'axios'],
       exclude: ['some-big-library']
     }
   });
   ```

6. **使用 CSS Modules**：
   ```css
   /* styles.module.css */
   .container {
     max-width: 1200px;
     margin: 0 auto;
   }
   ```
   ```javascript
   // component.jsx
   import styles from './styles.module.css';
   
   function Component() {
     return <div className={styles.container}>Content</div>;
   }
   ```

7. **合理使用插件**：
   - 只安装必要的插件
   - 优先使用官方推荐的插件
   - 定期更新插件版本

8. **启用 TypeScript 严格模式**：
   ```json
   // tsconfig.json
   {
     "compilerOptions": {
       "strict": true
     }
   }
   ```

## 参考资源

- [Vite 官方文档](https://vite.dev/guide/)
- [Vite 插件列表](https://vite.dev/plugins/)
- [Rollup 官方文档](https://rollupjs.org/guide/en/)
- [esbuild 官方文档](https://esbuild.github.io/)
- [Vite GitHub 仓库](https://github.com/vitejs/vite)
